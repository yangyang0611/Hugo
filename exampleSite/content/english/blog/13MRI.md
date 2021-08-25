---
title: "P4 13: MRI"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/ARPsproof.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

## **What is MRI?**
---
MRI，全名Multi-Hop Route Inspection，是可以讓 user 追蹤路徑與 queue 的長度的通訊種類

一個簡單的 mri.p4 需要以下的原件 :
1. ethernet_t ipn4_t ipv4_option_t mri_t and switch_t 的header定義
2. parser 來 parse 上述的 header
3. 一個用來丟棄封包的 action mark_to_drop()
4. 簡單的 ipv4 forward 來傳送封包
5. 一個 ingress control 定義一個 table 來選擇丟棄或傳送
6. 一個 control 在封包出去時會將 switch ID 與 queue depth 加上
7. 一個 egress control
8. deparser
9. package

&nbsp;
## **Topology**
---
![](https://imgur.com/OmGhOGEl.jpg)

首先新增 header
```c++
struct headers {
    ethernet_t         ethernet;
    ipv4_t             ipv4;
    ipv4_option_t      ipv4_option;
    mri_t              mri;
    switch_t[MAX_HOPS] swtraces;
}
```

再將Parser的邏輯建立好<br>
![](https://imgur.com/w0llmzrl.jpg)

接下來的 ingress control 就只是基本的 forwarding

egress comtrol 裡要將switch 的追蹤寫好
1. mri.count +1 (經過switch數量+1)
2. 因為要紀錄switch ID 所以要 push 新的 switch_t header 進去 swtraces
3. 根據 p4_16 spec 放東西進去是 invalid 所以要 hdr.swtraces[0].setValid()
4. 設定好 switch_id 跟 depth
5. ipv4 裡的 ihl 要增加 2 (internet header length)
6. optionlen 跟 totallen 要+8

&nbsp;
## **執行結果**
---
在 h2 執行 ./recieve.py<br>
在 h22 執行 iperf -s -u<br>
在 h1 執行 ./send.py 10.0.2.2 "test MRI" 30<br>
<font color=#00800>
**後面30秒時傳30秒**
</font>

在 h11 執行 iperf -c 10.0.2.22 -t 15 -u<br>
<font color=#00800>
**15是15秒傳一次**
</font>

當有iperf傳輸時因為s1跟s2之間只有一條通道 所以會看到 depth比較大<br>
![](https://imgur.com/HUfVUUI.jpg)

如果沒有iperf時 qdepth就會是空的<br>
![](https://imgur.com/OjCcizZ.jpg)

&nbsp;
## **IPERF**
---
Iperf 是一個 TCP/IP 和 UDP/IP 的性能測量工具<br>
能夠提供網路吞吐率訊息，以及震動、丟包率、最大段和最大傳輸單元大小等資訊

**參數說明 :**
- s 以server模式啟動
- u 以UDP封包代替TCP封包
- t 每隔多少秒傳輸一次 (default=10)
- c host以client模式啟動，host是server端地址
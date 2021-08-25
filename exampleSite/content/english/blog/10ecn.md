---
title: "P4 10: ECN 顯示拥塞通知"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/explicit_congestion.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

## **What is ECN?**
ECN 全名 Explicit Congestion Notification 顯式擁塞通知，是一個對IP和TCP的擴充。<br>
TCP/IP 在傳輸封包時，會在通道阻塞時丟棄封包。<br>
如果這時候有開啟ECN功能，ECN 的 router 會在IP的 header 中設定一個標記來代替丟棄封包，以告知阻塞即將發生。封包的接收端回應傳送端的表示，降低其傳輸速率，以避免封包遺失<br>

&nbsp;
### **IP 中的 ECN 操作**
ECN 使用 IPv4 header或 IPv6 header 中 ToS (Type of Service) 欄位的兩個最低有效位（最右側的位編碼）來表示四個狀態：
- **00 ：** 不支援 ECN 的傳輸，非 ECT(Non ECN-Capable Transport)
- **10 ：** 支援 ECN 的傳輸，ECT(0)
- **01 ：** 支援 ECN 的傳輸，ECT(1)
- **11 ：** 發生擁塞，CE(Congestion Encountered)

<center>

![](https://imgur.com/OjbAg1H.jpg)
</center><p>

當兩端支援 ECN 時，它將封包標為 ECT(0) 或 ECT(1)。
如果封包穿過一個遇到阻塞並且 router 支援 ECN 的 AQM 佇列，它可以將代碼更改為CE而非丟包。

<font color="#4F4F4F">

**AQM : Active queue management<br>
AQM常在 routers 跟 switches 使用到，為了要保持通道暢通跟降低 latency ，會將封包丟進一個 buffer 暫存。**</font>

這種行為就是「標記」，其目的是通知接收端即將發生擁塞。在接收端，該擁塞指示由上層協定（傳輸層協定）處理，並且需要將訊號回傳給傳送端，以通知其降低傳輸速率。

因為 CE 指示只能由支援它的上層協定有效處理，ECN 只能配合上層協定使用。例如 TCP 協定，它支援阻塞控制並且有方法將 CE 指示回傳給傳送端。

&nbsp;
### **TCP中的ECN**
TCP header 中的三個 flag 來支援ECN。第一個 flag 是隨機和（NS），另外兩個用於回傳擁塞指示（即指示傳送者應減少資訊傳送量）和確認接收到了擁塞指示回應(ECE跟CWR)。

<font color="#4F4F4F"><b>
- 隨機和 (Nonce Sum) : 用於防止TCP傳送者的封包標記被意外或惡意改動
- ECN-Echo（ECE） : 在 TCP 三方信號交換程序期間，TCP 對等體具備 ECN 功能
- Congestion Window Reduced（CWR） : 由傳送主機設定，指出已接到設定 ECE 旗標的 TCP 區段</b></font>

當在一個 TCP 連接上 ECN 後，傳送方指示連接上的TCP packet 攜帶 IP 分組傳輸流量，將支援ECN的傳輸用ECT碼做標記。可以使支援ECN的中間 router 可以標記具有 CE 碼的 IP 分組而不是丟棄它們，以指示即將發生的阻塞。

當接收到具有遇到阻塞碼的封包時，TCP接收者使用TCP頭中的ECE標記回傳這個阻塞指示。當一個端點收到TCP帶有ECE位的 header 時，它減少其擁塞窗口來代替丟包。

<center>

![](https://imgur.com/ICqk1jYl.jpg)
</center>

&nbsp;
## **Topology**
![](https://imgur.com/QghHay9l.jpg)
ECN.p4 需要以下這些元件

1. Ethernet 跟 IPv4 的 header
2. Ethernet 跟 IPv4 的 parser
3. 用來丟棄封包的 action mark_to_drop()
4. 基本 ipv4 foward 的 action
5. 一個 egress control 來檢查 ECN 跟 standard_metadata.enq_qdepth 還有設定 ipv4.ecn
6. 一個 deparser 將 fields 以正確順序放入要出去的 packet
7. 一個 package instantiate
將 ipv4 header 其中 8-bit 的 tos 再細分成 2-bit ECN 與 6-bit diffserv

```python
/*bit<8>    tos*/
bit<6>    diffserv;    
bit<2>    ecn;
```

在egress新增control判斷如果ECN==1 或 2 會比較 **standard_metadata.enq_qdepth** 跟 threshold 如果比較把再設定 **hdr.ipv4.ecn** 為 3
![](https://imgur.com/PnoG2tMl.jpg)

在 **MyComputeChecksum()** 修改 tos 新增 diffserv 跟 ecn
```python
/*hdr.ipv4.tos,*/
hdr.ipv4.diffserv,
hdr.ipv4.ecn,
```	
完成後執行 **make**建立mininet
執行**xterm h1 h2 h11 h22**
分別在h1 h2 執行<br>
**send.py 10.0.2.2 "steven is cool 30"** 跟 **recieve.py**<br>
注：send.py 後的 30 是 封包傳送 30 秒的意思

分別在h11 h22 執行 **iperf -c 10.0.2.22 -t 15 -u** 跟 **iperf -s -u**<br>
可以看到h2的recieve 封包裡的 tos值在 iperf 開始時會變成 3<br>
iperf 結束後會變成 1<br>
![](https://imgur.com/S1dUfsB.jpg)
![](https://imgur.com/bHPbdNZl.jpg)
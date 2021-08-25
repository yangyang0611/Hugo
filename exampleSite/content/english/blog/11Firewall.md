---
title: "P4 11: Firewall"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/ARPsproof.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

## **Topology**
![](https://imgur.com/2aO4oUSl.jpg)
firewall.p4需要有以下的components:

1. Ethernet (ethernet_t), IPv4 (ipv4_t) and TCP (tcp_t) 的header
2. Ethernet (ethernet_t), IPv4 (ipv4_t) and TCP (tcp_t) 的parser
3. 一個action來丟丟棄封包
4. 一個action來運算bloom filter的兩個hash
5. 基本的ipv4 forwarding
6. 一個action來設置一個變數來存action的參數
7. 一個table來讀封包的ingress和egress並且使用到 6. 的action
8. 一個control用來
9. 一個deparser用來emit Ethernet (ethernet_t), IPv4 (ipv4_t) and TCP (tcp_t) 封包
10. 一個 package instantiation

這個 firewall 可以將來自外部的 host 阻擋而內部的h1 h2可以自由連接
![](https://imgur.com/1IXzjspl.jpg)

首先會先檢查這個封包在 check_ports有沒有hit<br>
有的話就會進入 compute hash<br>
之後會分這個分包是從internal 還是 external 來的

如果是 internal 會再看有沒有 syn<br>
有的話就會重新設定 bloom filter

如果封包是 external就會讀取bloom filter<br>
如果兩邊的flow entries都有設定便會讓封包通過<br>

執行 **make run** 建立mininet<br>
執行 **iperf h1 h2** 會看到h1 h2有成功連線<br>
執行 **iperf h1 h3** 也會看到h1 h3有連線<br>
執行 **iperf h3 h1** 會沒有東西因為被firewall擋住外部的連線
![](https://imgur.com/Mxl936gl.jpg)

如果沒有 firewall 執行結果會是下圖<br>
![](https://imgur.com/Sl19ZrJl.jpg)<br>
**Figure: iperf h3 h1有連線**
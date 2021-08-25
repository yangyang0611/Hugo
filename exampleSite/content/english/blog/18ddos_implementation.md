---
title: "P4 18: DDoS Implimentation"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/ARPsproof.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

## **DDoS防禦攻擊:**
1. SYN Flood
2. UDP Flood
3. DNS Amplification
4. ICMP Flood
5. SYN-ACK Flood

### **Topology**
![](https://imgur.com/2aO4oUSl.jpg)

&nbsp;
### **攻擊方法**
透過scapy 傳送特定種類的封包

<u>**SYN/ACK Flood :**<br></u>
<font color ="4F4F4F">
**pkt = pkt /IP(dst=addr) / TCP(dport=1234, sport=random.randint(49152,65535))** </font>

<u>**UDP Flood :**<br></u>
<font color ="4F4F4F">
**pkt = pkt / IP(dst=addr) / UDP(sport=53)**</font>

<u>**DNS Amplification :**</u><br>
<font color ="4F4F4F">
**pkt / IP(dst=addr) / UDP(sport=random.randint(49152,65535),dport=53) / DNS(id = 111,qr = 0,opcode = 0,rd = 1**</font>

<u>**ICMP Flood :**</u><br>
<font color ="4F4F4F">
**pkt /IP(dst=addr) / ICMP(type=0)**</font>

type=0 為 echo reply

因為現今的DDoS攻擊大多都為多種層面的DDoS攻擊，大多都會是類似syn搭配udp的dynamic攻擊，所以需要考慮到同時出現不同protocol的攻擊

&nbsp;
### **防禦方法**
<u>**Syn Flood :**<br></u>
<font color ="4F4F4F">
**檢視通過的封包裡，syn跟ack的數量為一致的
如過syn跟ack的數量超過一個值(syn_limit)就會將封包drop**</font>

<u>**UDP Flood :**<br></u>
<font color ="4F4F4F">
**檢視通過的封包裡，udp封包的數量在一個值之下(udp_limit)**</font>

<u>**DNS Amplification :**<br></u>
<font color ="4F4F4F">
**先利用dns封包中的qr欄位判斷是查詢還是回應封包。若為查詢，利用dns封包中的transaction id與source ip的值來紀錄此封包的查詢。若為回應，就去看有沒有查詢紀錄，沒有的話便將此封包過濾掉。**</font>

<u>**ICMP Flood :**<br></u>
<font color ="4F4F4F">
**檢視通過的封包裡，udp封包的數量在一個值之下(icmp_limit)**</font>

<u>**SYN/ACK Flood :**<br></u>
<font color ="4F4F4F">
**檢視通過的封包裡，tcp封包裡syn-ack的數量在一個值之下(synack_limit)**</font>

&nbsp;
### **Result**
正常情況下 h2 傳送封包給h1 可以接收到<br>
![](https://imgur.com/65w5yP6.jpg)<br>
**Figure: node2 window**

![](https://imgur.com/tJ1zguf.jpg)<br>
**Figure: node 1 window**

被攻擊的時候 h2 封包傳送不到 h1<br>
![](https://imgur.com/65w5yP6.jpg)<br>
**Figure: node2 window**

![](https://imgur.com/tJ1zguf.jpg)<br>
**Figure: node1 window**

開啟防禦可以將DDoS緩解下來<br>
雖然還是有attack封包出現，但是h1已經可以接收到h2的訊息了<br>
![](https://imgur.com/VtRpsTx.jpg)<br>
**Figure: node2 window**

![](https://imgur.com/noDTCto.jpg)<br>
**Figure: node1 window**

有DNS回應封包傳入，但沒有曾經請求的紀錄所以被擋下來，沒有收到。<br>
![](https://imgur.com/jkx0i8pl.jpg)

測試host送出請求封包<br>
![](https://imgur.com/Z0WGTvol.jpg)

收到回應封包時，因為曾經有請求紀錄，所以沒有被擋下。<br>
![](https://imgur.com/hrOWd6wl.jpg)
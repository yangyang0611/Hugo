---
title: "P4 15: Type of DDoS"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/type_of_ddos.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

## **What is DDoS?**
---
DDoS 全名 distributed denial-of-service ，是一種網路攻擊手法，用多個電腦當作「殭屍」向一個特定的目標發動DoS式攻擊

<font color=#4F4F4F>

**| Dos : denial-of-service 阻斷服務**</font><br>
DoS會對目標發送大量的封包或請求，使得目標系統不堪負荷，達到影響目標系統的目的

DDoS 攻擊大致分為以下幾種 :
- UDP Flood
- ICMP (PING) Flood
- SYN Flood
- Ping of Death
- Slowloris
- NTP Amplification
- HTTP Flood

### **UDP Flood**
UDP Flood 就是對目標灌入大量的 UDP 封包，目標是將任何的 port 癱瘓，讓 host 反覆地檢查這個 port 正在使用的應用程式 ， 因為並沒有應用程式再使用，所以會回傳一個 ICMP (destination unreachable) 封包
這個過程會占滿 host 的資源，導致 client 無法對 host 存取

### **ICMP Flood**
跟 UDP Flood 一樣，ICMP Flood 會將目標的資源用 ICMP echo Request 封包占滿，非常快且大量地傳送封包且不等待回應
這種攻擊可以把 incoming 跟 outgoing 的 bandwitdh 塞滿，因為目標系統通常都會回復 ICMP echo request 封包，導致整個系統慢下來或是無法使用

### **SYN Flood**
SYN Flood 這個攻擊是使用 TCP 三方交握的漏洞
<font color=#4F4F4F>

**| 每一個向 host 發送的 SYN request 都需要被一個 SYN-ACK 回復，然後再被傳送請求的 client 回傳 ACK reponse 來確認連線**</font>

在 SYN Flood 攻擊中，攻擊方會對目標傳送大量的 SYN request，但是並不會對回傳的 SYN-ACK 做任何回應，就會導致系統一直等待跟占用連線的空間，最後就無法再建立起連線

### **Ping of Death**
POD 攻擊通常會對目標傳送大量畸形且惡意的 ping

<font color=#4F4F4F>

**| 一個封包最大的長度(包含 header )大概是 65,535 bytes，但是 data link layer 通常會設定一個最大的框架來限制封包(像是 1500 bytes over ethernet)，所以太大的封包就會會被切割成數個封包傳送，然後在接收端再將封包重組**</font>

在發生 Ping of Death 時，會在接收端收到許多惡意的封包碎片，導致在最後會重組成一個超過 65,535 bytes 的 IP 封包，會使 memory buffer overflow ， 造成系統癱瘓

### **Slowloris**
Slowloris 是一個 high targeted attack，讓一個 seb server 在不影響目標其他服務和 ports 的前提下癱瘓目標

<font color=#4F4F4F>

**| high targeted attack : 故意長時間且不被偵測地待在一個系統裡執行原本的設定好的作業** </font>

slowloris 攻擊會將與目標的連線打開越久越好，slowloris 做到這個的方法是在成功連線到目標時只傳送部分的 request<br>
slowloris 會不斷地項目標傳送 http 封包，但就是不完成任何 request，會導致目標一直將錯誤的連線開著，導致最後會 overflow maximum connection pool

### **NTP Amplification**
<font color=#4F4F4F>

**| NTP : Network Time Protocol，可以將使用這個 protocol 的網路裡所有的裝置進行時間的同步**</font>

在 NTP Amplification 攻擊中，攻擊者會使用 public-accessible NTP servers 的漏洞去將目標系統塞滿 UDP 的封包<br>
這個攻擊會是 amplification 攻擊是因為這個攻擊的 詢問-回應比例大概是在 1:20 ~ 1:200，所以這可以讓攻擊者使用一連串 public NTP server 產生一個超出負荷大體積的 DDoS 攻擊


### **HTTP Flood**
在 HTTP Flood 攻擊裡，攻擊者會大量傳送「看似合法」的 HTTP GET 或 POST 請求來攻擊目標系統<br>
HTTP Flood 不使用畸形封包、spoofing or reflection 技巧，需要癱瘓目標系統的 bandwidth 也比較小<br>
這個攻擊最顯著的時候就是強制系統對每一個 request 都要分配到最大的資源
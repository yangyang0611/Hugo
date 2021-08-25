---
title: "Transport Layer 傳輸層"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/transport_layer.jpg"
tags: ["Internet",]
description: "This is meta description."
draft: false
---

### **Multiplexing & Demultiplexing**
拆工&組工

![](https://imgur.com/iio4gvR.jpg)

### **UDP Checksum**
sender 把資料切割，相加。如果有超過 string，再相加。<br>
接著轉成1's complement，放在切割資料的最前端。

receiver 把資料加起來，如果ans＝1111...1，資料正確。
![](https://imgur.com/MCX3Ljkl.jpg)

### **TCP Fast Transmission**
儅 receiver 在 time out 前收到3個以上的 duplicate ACK (代表此 package 為 lost)，在time out 前重送 lost 的 package<br>
![](https://imgur.com/VBPYlk8.jpg)

### **TCP Flow Control**
receiver 會告訴 sender 自己有多少 free space buffer, sender 不要一直送 ACK (不然會空間不足)<br>
![](https://imgur.com/M5flh3Wl.jpg)

### **TCP Slow Control**
![](https://imgur.com/KlOe0nQl.jpg)

### **TCP Reno**
![](https://imgur.com/S2sQJ6C.jpg)

### **ENC(Explicit Congestion Control)**
client 在 package header 中添加一個 ECT(ECN Capable Transport)，儅發生 congestion, package 會被設成EC。sender 收到後回傳 EC-ENCO, client 下一次送 package 就會避免走冤枉路<br>
![](https://imgur.com/PBJPbUhl.jpg)
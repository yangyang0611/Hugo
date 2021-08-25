---
title: "SDN Types"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/sdn.jpg"
tags: ["Internet","Security"]
description: "This is meta description."
draft: false
---

## **SDN分類**
- 7層網絡協議（OSI）
- 5層網絡協議（TCP/IP）
- 4層網絡協議（DoD）

&nbsp;
### **7層網絡協定（OSI)**
<center>

![](https://imgur.com/Pj0Qstk.jpg)<br>
**figure：OSI7層網路架構圖**
</center>

#### **Application Layer圖形化界面 (Layer 7)**
- **HTTP ：** 瀏覽網頁
- **SMTP ：** 電子郵件
- **FTP  ：** 傳送檔案
![]()

#### **Presentation Layer (Layer 6)**
![]()

#### **Session (Layer 5)**
![]()

#### **Transpotation (Layer 4)**
###### Client -> Server Architecture
TCP (Transmission Control Protocol）: 3-way handshaking , 回傳 SYN & ACK

**3-way handshaking:** <br>
1. client -> server -> client (read & write `裝進 socket buffer 裏面傳`)
2. client write buffer -> internet -> server read buffer
3. server write buffer -> internet -> client read buffer

#### **Network Layer網路層（Layer 3）**
`Router` 添加 IP address （IPv4 / IPv6）

#### **Link Layer連接層（Layer 2)**
`Swtich` 添加 mac address
- ATM(Asynchronous Transfer Mode) : 傳輸量小，傳語音
- PPP(Point-to-Point Protocol)：.......

#### **Physical Layer硬體層（Layer 1)**
由 hub，網路綫，光纖等硬體傳輸媒介

&nbsp;
### **5層網絡協定（TCP/IP)**
<center>

![](https://imgur.com/7l53NLG.jpg)
</center>

&nbsp;
### **4層網絡協定（DoD)**
![](https://imgur.com/7bXzKtcl.jpg)
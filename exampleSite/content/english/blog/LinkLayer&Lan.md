---
title: "Link Layer連接層 & Lan"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/data_link.jpg"
tags: ["internet",]
description: "This is meta description."
draft: false
---

## **What is Link Layer?**
Link layer是網路層的第2層，提供的服務有以下幾項:
- **flow control:** 使相鄰sending 和 receiving node 步調一致
- **error detections:** 儅錯誤發生時(如package lost)，接收端可以及時detect error，並請求sender重新發送封包
- **error corrections:** 獲取identifies、在不請求重新連綫的情況下改正bit errors
- **half-duplex and full-duplex:** half-deplex讓link末端的nodes可以在不同時間點互相傳遞 

&nbsp;
## **Multiple Access Protocol**
---
### **Sorted Aloha**
1. channel idle - 拿到data，在機率p送
2. channel collision - 在機率p送

<u>**好處**</u>
- 一個node可以一直占據channel，直到node送完讓別人送
- simple

<u>**壞處**</u>
- 送的機率為p，所以有可能channel是empty的，浪費
- p一樣的時候，會發生collision

&nbsp;
### **Pure Aloha**
有data就馬上送，效率最爛

&nbsp;
### **CSMA（Carrier Sense Multiple Access**
listen before transmission
1. channel idle - 馬上傳（node1 —> node4，node1判斷channel idle要傳，但有propagattion delay真正傳出去的時間不一樣，node4在這時判斷沒人所以決定傳）<br>
2. channel busy - 延遲傳送

&nbsp;
### **CSMA/CD（Collision Detection）**
一邊傳一邊listen有無collision，有的話先停止傳輸
1. 網卡(NIC)從network layer取得frame
2. NIC判斷idle，開始傳。Busy，等待idle開始傳
3. 沒有collision發生，成功！！
4. 有collision，暫停，告訴所有人channal busy狀態
5. NIC進行binary（exponential）backoff：等待第2^（m-1）時間再傳輸
    - 第1次collosion，等待0sec
    - 第2次collosion，等待2sec …… (一次類推)
      *** 等待的時候發現有人傳，暫停倒計時，結束後才接著往下count down

&nbsp;
### **CSMA/CA(Collision Advoidance)**
<u>**Sender**</u><br>
- **channel idle:** 等待DIFS時間，時間到送package
- **channel busy:**
    1. random time之後送package
    2. 儅count down時候遇到channel busy, stop count down wait until 別人送完
    3. 從上一個號碼繼續往下count down，算完后送
    4. 如果沒有ACK（代表package丟失），重複2

<u>**Receiver**</u><br>
收到package后，等待DIFS時間后，回傳ACK（爲了判斷有沒有hidden terminal problem）

&nbsp;
### **"Take Turns" MAC Protocols**
##### **A. Polling**
master一個個問slave，有人要送嗎？<br>
1. **有:** 送
2. **沒有:** 問下一台電腦， 問完一圈又重頭問起<br>
![](https://imgur.com/6QWp5CG.jpg)

##### **B. Token Parsing**
token一個個以圓形的軌跡pass token，收到token的電腦有要送資料嗎？
1. **有：** 送
2. **沒有：** token pass to下一台電腦， pass完一圈又重頭pass起<br>
![](https://imgur.com/yEMb7G4.jpg)

&nbsp;
### **APR (Address Resolution Protocol)**
ARP table中記載了internet topology裏所有pc的ip address 和 MAC address。<br>
儅pc1 傳資料給 pc2，但pc1不知道pc2的macAddr，只知道ip address時，他將向Internet的所有pc發送broadcast封包。這時，所有pc會檢查broadcast的destAddr與自己的macAddr是否一致，不一樣就drop，只有pc2匹配成功。<br>
最後，pc2向pc1回傳時一并把自己的MAC address加入ARP table中。<br>
**通過這個方法，switch能夠self-learning知道所有人的MAC address**
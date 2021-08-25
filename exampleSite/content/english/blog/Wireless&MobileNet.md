---
title: "Wireless & Mobile Net"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/wireless.jpg"
tags: ["internet"]
description: "This is meta description."
draft: false
---

### **802.11 Passive Scanning/Active Scanning**
<u>**Passive Scanning**</u><br>
AP跟電腦說自己的存在，電腦需要可以跟我連接哦！<br>
電腦請求其一連綫，其一發送確認連接消息給電腦

<u>**Active Scanning**</u><br>
電腦需要傳資料時，主動跟AP請求，AP1發送（我可以提供協助哦！）給電腦<br>
電腦請求其一連綫，其一發送確認連接消息給電腦

&nbsp;
### **DFC 分散式網路系統**
沒有中央控制器的網路

DFC基於CSMA，使用RTS/CTS握手作爲訪問方式<br>
<u>好處：</u>可靠、易擴充<br>
![](https://imgur.com/NdETTL2l.jpg)

&nbsp;
### **PEC 集中式網路系統**
有中央控制器的網路

&nbsp;
### **IFC (Interframe Space)**
- **SIFS:** 最短時間區隔，用來間隔（RTS/CTS/ACK），防止其他等待node用到channel
- **PIFS:** 只能用PCD system的node使用
- **DIFS:** 只能用DCF system的node使用
- **EIFS:** 在channel collision, node delay EIFS 而不是DIFS time，在發送下一批

&nbsp;
### **Stop and Wait**
每傳完一個package先stop，收到對方的ACK后才下一個package傳輸`（RELIABLE!!）`<br>
![](https://imgur.com/5FIWJ7Cl.jpg)
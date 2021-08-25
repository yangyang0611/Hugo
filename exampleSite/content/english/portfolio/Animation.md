---
title: "Animation Displayer"
date: 2021-07-30T12:14:34+06:00
image: "images/portfolio/animation_displayer.jpg"
categories: ["design","development","hardware"]
description: "This is meta description."
draft: false
project_info:
- name: "Collaborator"
  icon: "fas fa-user"
  content: "In a group of 4"
- name: "Project Link"
  icon: "fas fa-link"
  content: "https://github.com/yangyang0611/Animation-Displayer"
- name: "Report"
  icon: "fas fa-file"
  content: "https://drive.google.com/file/d/1yKgkV8yetxpzdiAUIT2Pp-EiFcY0tLF4/view?usp=sharing"
- name: "Demo Link"
  icon: "fas fa-video"
  content: "https://youtu.be/1ZEaAyQWCzQ"
---

系統功能為動畫故事撥放器。
以點矩陣作為故事書的畫面，UART 作為故事的文字內容，ADC 作為控制頁數的功能。

### **系統使用環境及對象**
- **使用環境：** mpLab
- **對象：** xc8

### **Appearance**
![](https://i.imgur.com/73gXQOJl.jpg)

![](https://i.imgur.com/h9vgquRl.jpg)<p>

&nbsp;
### **Circuit Diagram**
![](https://i.imgur.com/jNgUHhGh.png)

![](https://i.imgur.com/AGMBnX1h.png)

&nbsp;
### **Flow Chat**
![](https://i.imgur.com/1QwORoLh.jpg)<p>

&nbsp;
### **系統開發工具、材料及技術**
- **工具：** MPLab， Pickit4 燒錄器, PIC18f4520 晶片, 8x8 點矩陣, 可變電阻,
TTL 線，麵包版<br>
- **技術：** 利用轉動可變電阻來產生 Interupt。在 interupt service routine 裏，利用 ADRES 的值去改變圖形位置。通過計算可變電阻的旋轉範圍，對應該範圍下，矩陣產生的圖案，並搭配 UART 讓熒幕產生相對應的文字敘述。

&nbsp;
### **周邊接口或 Library 及 API 使用說明**
- **Interrupt:** UART CCP
- **UART:** 使用 UART 輸出文字
- **ADC:** 利用 0 到 255 的區間控制故事圖片流程

&nbsp;
### **遇到的困難及如何解決**
##### **1.	音效同步問題**
原本是打算隨著動畫移動，在外部連接揚聲器同步播放音效，但由於聲音在播放中會遇到大量 delay 問題，無法跟上同步訊號，導致嘗試了許多遍都宣告失敗

##### **2.	PORT 共用有問題**
點矩陣有兩個 pin 腳接到另外一個 PORT

##### **3.	ADC 與 UART 的 interrupt 互相衝突**
直接融合讀取 ADC 的值，再判斷並輸出到 UART

##### **4.	按鈕**
一開始的設計理念中，我們打算運用按鈕觸發 Interupt 產生。儅試著把按鈕接 interupt pin(RB0)上，卻沒辦法讓程式成功進到 interupt service routine 裏。因此改用ad converter 取代按鈕

##### **5.	點矩陣銀幕閃爍**
每一張圖片在矩陣切換過程中，我們會用 delay 函數去控制發生的時間差 。由於切換操作是用 while loop 包起來，所以在還沒轉移到下一張圖片時，while loop 會一直進行導致銀幕閃爍不停。我們嘗試拉長 delay 頻率或縮短頻率也無法解決，最後搭配 UART 銀幕便停止閃爍了

##### **6.	無法隨機 random 出數字** 
由於 c++在 mplab 中無法成功 random 出數字，解決辦法是自己寫一個非常大的 array 去存取隨機變數

##### **7.	公母綫損壞**
在連接外部裝置時，常遇到裝置無法成功操作。爲了抓出問題，常使用三用電表對每一根電綫做通電判斷
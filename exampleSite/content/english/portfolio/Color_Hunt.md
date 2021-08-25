---
title: "Color Hunter"
date: 2020-11-06T12:14:34+06:00
image: "images/portfolio/color_hunter.jpg"
categories: ["design","development"]
description: "This is meta description."
draft: false
project_info:
- name: "Collaborator"
  icon: "fas fa-user"
  content: "In a group of 4"
- name: "Project Link"
  icon: "fas fa-link"
  content: "https://github.com/yangyang0611/Color_Hunter"
- name: "Report"
  icon: "fas fa-file"
  content: "https://drive.google.com/file/d/16cUBg7wiMy5hEmL0ssEwly98uSxhVC6U/view?usp=sharing"
---

Color Hunter是一款主打顔色辨識的小游戲。<br>
開發目的是爲了改善組員長期的辨色困擾，希望通過此游戲可以幫助她重回信心。

## **Project Details**
### **主頁面**
![](https://imgur.com/IREc8ie.jpg)<br>
游戲一開始會進入主頁面，有兩款游戲供選擇，分別是
- **猜不同顔色** 
- **文字顔色猜一猜** 
- **記錄**

### **猜不同顔色**
**游戲規則：玩家需要根據文字的背景色，點選下方的按鈕。**
![](https://imgur.com/qZ4O5dP.jpg)<br>
如圖所示：雖然文字是綠色，但文字的背景色是藍色，所以要點選藍色才是正確答案哦~

系統上方的score欄位會顯示目前得到多少分。一旦玩家點選到錯誤的答案會立刻結束游戲，並跳出輸入名字視窗，玩家姓名與游戲分數會記錄在後端資料庫内，可以通過主頁面的記錄按鈕進行查看。如果中途耐心被磨掉想要放棄游戲，便可以點選右上方的exit按鈕退出。

### **文字顔色猜一猜**
**游戲規則：玩家有30秒的時間，找出25個方格内1個與其他方格不同的顔色，共有10關卡。**
![](https://imgur.com/rUYOsW1.jpg)<br>
如圖所示：在這25個方格中，右下角的色塊明顯和大家不一樣，所以要點選他才能進入下一關哦~

游戲一開始所有方格都不具顔色，只有儅玩家按下start按鈕后，游戲開始方格顔色才會改變。<br>
- **level欄位:** 顯示目前是第幾關<br>
- **Time欄位:** 從30秒開始倒數，並顯示目前所剩的時間<br>
- **Marks欄位:** 顯示目前得到多少分，比分是根據闖關數量而定，一關一分<br>
- **exit按鈕:** 點選exit方可退出游戲。<br>

一旦玩家成功闖破10關便會跳出 **“恭喜你，成功了~”** 的視窗，並可以在視窗欄位中填入姓名。玩家姓名與游戲分數會記錄在後端資料庫内，可以通過主頁面的記錄按鈕進行查看。反之如果在30秒内無法順利闖關，則會跳出 **“時間到！輸入姓名”** 的視窗，玩家進度也會一并記錄到系統内。

### **記錄**
![](https://imgur.com/3U4x9hJ.jpg)<br>
有2個欄位供選擇，可以通過點選不同游戲欄位，看到玩家姓名及積分。

## **Project Archeivement**
把java課堂所學的知識運用到游戲中:
- Swing實作    
- 繼承
- 存檔讀檔功能
- Serialize
- 切換頁面
- 排名
- Timer & Random
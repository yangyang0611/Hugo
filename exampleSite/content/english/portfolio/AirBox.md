---
title: "PM2.5 Air Box"
date: 2021-07-30T12:14:34+06:00
image: "images/portfolio/airbox.jpg"
categories: ["design","development","hardware"]
description: "This is meta description."
draft: false
project_info:
- name: "Collaborator"
  icon: "fas fa-user"
  content: "In a group of 4"
- name: "Project Link"
  icon: "fas fa-link"
  content: ""
- name: "Demo Link"
  icon: "fas fa-video"
  content: "https://www.youtube.com/watch?v=9-TOrMKjFs4&t=3s"
---

空氣中分布著許多物質，其形態可分為固態、液態或氣態等等。就一般而言，粒徑小於10微米(μm)的粒子稱之為PM10，而粒徑小於2.5微米(μm)則為PM2.5。這類分子結構小的懸浮微粒，很容易透過鼻腔内膜的阻擋進入體内，造成人體器官不同的危害。因此我們設計出一款可以偵測空氣中PM2.5含量多寡的空氣盒子（PM2.5 Air Box)，提供及時性的空氣品質數據。

## **Project Details**
#### **設計**
我們使用xx軟體來設計空氣盒子的外形，并用3d printer印出成品。

爲了讓空氣流通，我們在盒子的最前端開了7孔，讓sensor探測到的空氣不局限於盒子内。<br>
另外，爲了穿戴方便，使用者可以在盒子後端的穿孔上繫上皮帶。出門時將皮帶繫在腰間，減少手握的負擔。頂部的蓋子也有夾縫設計，使其盒子本體完美貼合，以讓使用者在大幅度運動的狀態下（例如跑步等）不會發生機器錯位或掉出盒子的風險。

#### **内部構造**
- **供電：** sensor需要通電的情況下才可以正常使用，因此我們外接了一個電池
- **藍牙晶片：** 裝置可以透過藍牙與手機互通。儅藍牙未連接到手機，晶片的LED會顯示紅燈。等連接到了手機，LED燈會顯示紅燈並持續閃爍
- **空氣探測器：** 内部的小風扇會旋轉運行， 探測空氣
- **Arduino面板：** 操作裝置的主要電路板

## **Mobile App**
首先，使用者在手機主頁面上按下搜尋裝置按鈕，藍牙便會尋找裝置進行配對。<br>
接著到戶外活動。裝置會顯示及時的PM2.5顆粒濃度到手機頁面上。如果測出當前的空氣品質非常糟糕，便會出現“警戒等級”的字樣；反之良好的情況下則不會。
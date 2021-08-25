---
title: "Draw Doraemon using FFT"
date: 2021-07-2T12:14:34+06:00
image: "images/portfolio/Doraemon.jpg"
categories: ["design","development","matlab",]
description: "This is meta description."
draft: false
project_info:
- name: "Collaboration"
  icon: "fas fa-user"
  content: "Done in a group of 5"

- name: "Project Link"
  icon: "fas fa-link"
  content: "https://github.com/yangyang0611/Doraemon-Fourier-Transformation"
- name: "Report"
  icon: "fas fa-file"
  content: "https://drive.google.com/file/d/1rvXQWhRoUoNQBAcQrXm0L1L050q7vLT5/view?usp=sharing"
- name: "Demo Video"
  icon: "fas fa-video"
  content: "https://www.youtube.com/watch?v=C59EEE6kAqM"
---


## **Project Details**

&nbsp;
### **1. Drawing With Vector 向量作圖**
動機：想要借由傅里葉方程式（Fourier Transformation）作圖，並額外加上箭頭標記。
![](https://imgur.com/dp0k0K1l.jpg)*With vector -->* ![](https://imgur.com/PEBkfPLl.jpg)

&nbsp;
### **2. Complicated graphics 複雜圖形作圖**
##### **ALERT!!!** <br>
**NEED TO DOWNLOAD 'IMAGE PEOCESSING TOOLBOX' FROM MATLAB ADD-ON TOOLBAR.**<br>
Link: <a href="https://www.mathworks.com/products/image.html" target="_blank">Image Processing Toolbox of MATLAB</a>

由於FFT只能一筆畫出圖形，因此我們將加上BFS(Breath First Search)。將圖形坐標進行切割，並畫出複雜圖形。

**Simple FFT graph &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Target graph**<br>
![](https://imgur.com/i3aA40Wl.jpg) *simple --> hard* &nbsp;
![](https://imgur.com/ZzttRnnl.jpg)

**Algorithm:**<br>
![](https://imgur.com/97OD83Hl.jpg)

&nbsp;
### **3. Results and Dicussion 結果與討論**
- 要同時畫圖和箭頭電腦會很當
- 比起Matlab，應該使用python繪圖會更簡單
- 參數的調整

&nbsp;
#### A. **參數的影響 --- drop**
##### **drop=1 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; drop=5**<br>
![](https://imgur.com/4v4mCanl.jpg) &nbsp; &nbsp; &nbsp;
![](https://imgur.com/1NUxJGOl.jpg)


##### **drop=30 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; drop=50**<br>
![](https://imgur.com/ss20UPvl.jpg)
![](https://imgur.com/fXLIw0xl.jpg)

&nbsp;
#### **B. 參數的影響 --- interpolationM**
##### **M=1 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; M=3**<br>
![](https://imgur.com/6POPK4Yl.jpg) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
![](https://imgur.com/xUdhFDTl.jpg)

&nbsp;
#### **C. 參數的影響 --- pixel distance**<br>

<img src="https://media.giphy.com/media/kZWz98A96CSLC3RO2b/giphy.gif" width="300" height="260">
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
<img src="https://media.giphy.com/media/CcKSYu0HEGzty46TID/giphy.gif" width="300" height="260">

&nbsp;
#### **Result**
##### **Original &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Final**<br>
![](https://imgur.com/ZzttRnnm.jpg) &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
![](https://imgur.com/yfI4EP5l.jpg)

&nbsp;
##

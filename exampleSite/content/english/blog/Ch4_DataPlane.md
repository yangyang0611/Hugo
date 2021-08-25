---
title: "Data Plane"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/data_plane.jpg"
tags: ["internet"]
description: "This is meta description."
draft: false
---

網路層Network Layer是由Data Plane 和 Control Plane組成。

## **What is Data Plane?**
- 儅datagram到達router input port時，決定該如何將包forward到router output port（router間的輸入輸出）
-  forwarding function
- local, per-router function

## **What is Control Plane?**
- 如何決定這個datagram到達目的地的路徑（datagram在整個router topology上的傳輸路徑）
- routing algorithm
- network-wide logic
    - 傳統routing algorithm
    - SDN

![](https://imgur.com/NoQCUz8.jpg)

## **What is inside a router?**
---
### **Switching Fabries**
transfer package from input buffer to appropriate output buffer.<br>
There are three types of switching buffer:<br>
![](https://imgur.com/YuVrVYo.jpg)
![](https://imgur.com/iIFqYNJ.jpg)
![](https://imgur.com/tSfBsGV.jpg)

##### **Switching via memory**
- 封包存放在system's memory
- memory bandwith 的限制速度為2bus/datagram
![](https://imgur.com/KtFZn86.jpg)

##### **Switching via bus**
- datagram form input port memory to output port memory via a shared bus
- switching speed limited by bus bandwitch

##### **Switching via interconnection network**
- 解決bus bandwidth limitation問題
- 把datagram切割成固定長度，在fabric中傳輸

&nbsp;
## **Scheduling Mechanisms**
---
#### **First In First Out(FIFO)**
discrad policy: 如果queue滿了，又有新的封包到達，該怎麽辦？
- **Tail drop：** 丟棄新封包
- **Priority Scheduling：** 丟棄優先權低的封包
- **Random：** 隨機丟棄封包<br>
![](https://imgur.com/jAIrVqel.jpg)

#### **Priority Scheduling**
如下圖：high priority封包存放在(紅色queue)、low priority封包存放在(綠色queue)<br>
![](https://imgur.com/ZvNeXO9.jpg)<br>

如下圖：封包1、2、3到達，由於紅色是high priority，因此queue1、3，送出1、3。最後才queue 2，送出2。<br>
接著新的packet4抵達，沒有封包跟他競爭所以queue4，送出4。<br><br>
![](https://imgur.com/64xnOtd.jpg)

#### **Round Robin(RR)**
- multiple classes
- 顔色交替queue、交替傳送

如下圖：packet1、2、3同時來。queue1送1；queue3，送3；queue2，送2 **（是送2底下圖片有誤）**<br>
![](https://imgur.com/HpZkyHHl.jpg)

#### **Weighted Fair Queuing(WFQ)**
如下圖：假設packet1(weight=0.4),packet2(weight=0.2),packet3(weight=0.4)<br>
那麽output根據weight大小送出<br>
![](https://imgur.com/y5Goq8u.jpg)<br>
output: red->blue->green 或者 blue->red->green

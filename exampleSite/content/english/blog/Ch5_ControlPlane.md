---
title: "Control Plane"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/control_plane.jpg"
tags: ["internet"]
description: "This is meta description."
draft: false
---

#### **Recall two network functions:**
- **forwarding:** 移動封包從router input -> router output `(Data Plane)` 
- **routing:** 決定封包從source -> destination的路徑 `(Control Plane)`

![](https://imgur.com/EsGzxqKl.jpg)

## **Type of Algothrim**
---
#### **1. Link State Algorithm**
用Dijkstra求出最短路徑

#### **2. Distance Vertor Algorithm**
>
Good news travels fast. Bad news travels slow
- 用Bellman-Ford Equation(Dynamic Programming)求解
- Link Cost Change
    - node detects locol link cost change 
    - uodate router info, recalculate distance vector
    - id DV change, notify neighbours

&nbsp;
## **Type of Network Connection**
---
#### **1. Inter Network Connection**
internet與internet做連接（外部連接）

#### **2. Intra Network Connection**
内部router與router做連接
- RIP(Routing Information Protocol)
- OSPF(Open Shortest Path First)
- BGP(Gateway Routing Protocol)

##### **Routing Information Protocol(RIP)**
- 规模较小的、可靠性要求较低的网络使用
- 通过不断的交换信息让路由器动态的适应网络连接的变化，这些信息包括每个路由器可以到达哪些网络，这些网络有多远等

##### **Open Shortest Path First(OSPF)**
- 小型區域網路使用（公園、辦公室..）
- 使用最短路徑求解（Dijkstra）
- 分層topology（boundary router, backbone router, area border router）
- 收斂時間小
- IP協議
![](https://imgur.com/GGcPWCK.jpg)
<center>

**figure: hirachy of OSPF**</center>

##### **Border Gateway Protocol(BGP)**
###### **---> iBGP(internal) & eBGP(external)**
- 大型網路使用（需要和其他network連接）
- 使用最佳解
- 網狀topology
- 收斂時間長
- TCP協議<br>

![](https://imgur.com/As75MSb.jpg)

&nbsp;
## **Types of Protocols**
---
#### **1. Hot Potato Protocol**
switch傳資料，走weight最小edge（最短路徑，就算cost(要經過的router數量多也無所謂))
![](https://imgur.com/CBLGNst.jpg)<br>
如圖所示：router 2d要返回AS3。走2c的cost為263，走2a的cost為201（weight較少），因此選擇走2a(`不在乎inter domain cost!`)

#### **2. Internet Control Message Protocol(ICMP)**
Echo request, Echo reply — by command line "ping (IP)"<br>
IF Destination Unreachable :<br>
- 代表request被firewall block
- ping to a 不存在IP address

#### **3. Simple Network Management Protocol(SNMP)**
host 詢問server一些問題，server如實回答(questions are very in details)<br>
注：只有SNMP devices才可以有SNMP request

eg: amount of traffics, configuration, status.. <br>
- **V1:** structures tables, no encryption
- **V2:** data type enhancements, bulk transfers, no encryption
- **V3:** encryption, authentication
---
title: "P4 02: Mininet"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/ARPsproof.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

## **What is Mininet?**
---
可以簡單地把Mininet當成是一個網路模擬器，會創造一個有virtual hosts、switches、controllers跟links的網路。透過mininet在自己的電腦上創造一個虛擬網路，然後以電腦來發送封包並且可以透過SSH登陸虛擬host操作。P4語言主要被運用在switch的控制上，開發者能夠直接定義出一個switch能夠處理的封包格式。
<center>

![](https://imgur.com/8oKKH8Ml.jpg)<br>
**Figure: mininet簡易架構圖**
</center>

&nbsp;
### **安裝環境過程**
---
一開始先將github(https://github.com/p4lang/tutorials)的repository clone下來，接下來安裝好vagrant跟virtualbox。Vagrant是一款用於構建及配置虛擬開發環境的軟體。在clone下來的vm資料夾裡面打上指令vagrant up就會把虛擬機所需要的資料下載完成了，過程大概一個小時。 之後就可以使用vagrant或是p4帳號進行登入。

<center>

![](https://imgur.com/NFivtOml.jpg)<br>
**Figure: 登錄畫面**
</center>

開啟terminal輸入mn就可以建立簡易的mininet網路
<center>

![](https://imgur.com/Mr6XD8El.jpg)<br>
**Figure: 建立Mininet網絡**
</center>

輸入不同指令可以進行不同的操作<br>
- **net：** 可以看到各鏈結的訊息<br>
h1 h1-eth0:s1-eth1<br>
h2 h2-eth0:s1-eth2<br>
s1 lo: s1-eth1:h1-eth0 s1-eth2:h2-eth0

- **nodes：** 可以印出所有節點<br>
available nodes are:<br>
c0 h1 h2 s1<br>

- **dump：** 可以看到各節點的訊息<br>
Host h1: h1-eth0:10.0.0.1 pid=8536<br>
Host h2: h2-eth0:10.0.0.2 pid=8539<br>
OVSSwitch s1: lo:127.0.0.1,s1-eth1:None,s1-eth2: None pid=8545<br>
OVSController c0:127.0.0.1:6653 pid=8529

<center>

![](https://imgur.com/eC3yFuql.jpg)<br>
**Figure：不同指令的功能**
</center>

輸入**h1 ping h2** 便可以從h1向h2發送封包<br>
<center>

![](https://imgur.com/LeeGQT6l.jpg)<br>
**Figure:h1 ping h2**
</center>

也可以將wireshark開啟監控封包轉發的情形
圖中有Source跟destination<br>
其中source 10.0.0.1 destination 10.0.0.2 為h1發送給h2的封包<br>
點開來可以看到詳細的資訊，例如使用IPv4<br>
<center>

![](https://imgur.com/6ehoZtjl.jpg)<br>
**Figure: wireshark監控封包**
</center>
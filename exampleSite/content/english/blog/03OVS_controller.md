---
title: "P4 03: OVS Controller"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/ovs_kernal.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

## **What is OVS?**
---
OVS全名 Openvswitch，是一個開源的交換器，也是實現網路虛擬化 SDN 的重要基礎，設計 OpenvSwitch 的目的是為了解決實體交換器存在的局限性，比實體交換器更低的成本和更高的工作效率，而 Openvswitch 本身佔用的資源也非常小，可以根據自己的選擇靈活的配置，可以對封包進行接收分析處理同時還支援標準的管理介面和協議，如 NetFlow，sFlow，SPAN，RSPAN 等。而OVS controller可以控制多個都是openflow協議下的交換器。

- **Netflow:** 一種網路監測功能，可以收集進入及離開網路界面的IP封包的數量及資訊。<br>
- **sFlow:** 運用取樣通訊協定並著重於處理個別資料封包，因此可以識別個別檔案是否已損壞或包含惡意程式碼。<br>
- **SPAN:** 全名The Switched Port Analyzer，獲得了源埠的MAC位址後，會將流經該MAC位址的所有資料直接發往目標埠。<br>
- **RSPAN:** Remote SPAN，當某些源口做為目標口出現時，不處於同一交換機上

&nbsp;
### **What is ICMP?**
---
ICMP 全名 Internet Control Message Protocol是網際網路協定套組的核心協定之一。它用於網際網路協定（IP）中傳送控制訊息，提供可能發生在通訊環境中的各種問題回饋。<br>

<center>

![](https://imgur.com/3I4OyzUm.jpg)<br>
**Figure：ICMP protocol**
</center>

&nbsp;
## **P4 入門**
---

<center>

![](https://imgur.com/OgH5gVal.jpg)<br>
**Figure:封包結構**
</center>

P4中有5個語言組件： Headers、parsers、Tables、Action、control program。
- **headers：** headers有分為兩種，一種是packet header另一種是metadata。
- **Parsers：** 一個p4程式往往定義了許多headers，但不是全部的headers都會對封包進行操作。Parser的工作就是會產生哪些封包進行了操作的intermediate representation。
- **Tables：** 當table中的欄位與封包配對成功時，就會執行相對應的工作。如果沒也成功配對則會標記成miss。
- **Actions：** 主要分為primitive action與compound action。Primitive actions包括封包的修改、基本運算、hash運算等等。Compound actions通常都由用戶自己定義。

<center>

![](https://imgur.com/ZgscuI9l.jpg)<br>
**Figure:P4程式架構**
</center>

### **進行簡單的P4 實驗**
---
要進行basic forwarding ，就是將ipv4封包往前傳送

使用的topology為下圖
![](https://imgur.com/9cs2SNgl.jpg)

編譯basic.p4 輸入**make run**

<center>

![](https://imgur.com/BP9nkVwl.jpg)<br>
**Figure: makefile 檔案**
</center>

看到最後一行include了utils資料夾裡的makefile<br>
可以看到執行的是一個寫好的script<br>
Script會執行一個由python寫好的run_topology.py<br>

<center>

![](https://imgur.com/t1xCePVl.jpg)<br>
**Figure: 找到make run 程式碼對應的動作**
</center>

make run指令將會
1. 編譯basic.p4
2. 建立mininet，其中有4個host，各自連接一個switch
3. Host的IP分別為10.0.1.1, 10.0.2.2, 10.0.3.3,10.0.4.4

<center>

![](https://imgur.com/ZdtcIwbl.jpg)<br>
**Figure: 執行完makerun**
</center>

這時候看到使用的switch已經不是上次的預設ovs switch<br>

<center>

![](https://imgur.com/NXkYQHbl.jpg)<br>
**Figure:  configuredP4Runtime switch**
</center>

此時如果輸入h1 ping h2<br>
成功的話會顯示道有收到封包<br>

<center>

![](https://imgur.com/nEHtB8cl.jpg)<br>
**Figure: 成功收到封包**
</center>

失敗就不會顯示

<center>

![](https://imgur.com/He01wAel.jpg)<br>
**Figure: 沒有收到封包**
</center>
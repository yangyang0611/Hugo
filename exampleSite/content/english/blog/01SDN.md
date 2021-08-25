---
title: "P4 01: SDN 軟體定義網路"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/sdn2.jpg"
tags: ["internet"]
description: "This is meta description."
draft: false
---

## **What is SDN?**
---
SDN全名software define network，是一種網路設計理念、網路架構。以OSI 7層來看，SDN大多是在處理第2跟第3層。<br>

<center>

![](https://imgur.com/zZjV06f.jpg)<br>
**Figure：OSI7與TCP/IP架構圖**
</center><p>

&nbsp;
### **SDN三大架構**
---
- Application Layer
- Control Layer
- Infrastructure Layer

SDN會將router的 **control plane(routing、ARP、DHCP)** 與 **data plane(IPv4、IPv6)** 分開，交給controller的軟體負責。SDN存在的目的就是簡化過多的網絡結構，通過抽象出來的數據原始描述作為可編程最小元素，對這些所有的元素排列組合，定製轉發邏輯，使轉發層面集群，按照定製的規則轉發數據。

<center>

![](https://imgur.com/oN9hqqn.jpg)<br>
**Figure ：OSI7與TCP/IP架構圖**
</center><p>

&nbsp;
### **SDN三個大優勢**
---
- 降低成本
- 提高效率
- 安全穩定

在相同的功能，透過SDN運行的伺服器所承擔的成本遠遠低於硬體設備。SDN網路架構在進行升級的時候，網路配置的時間也低於傳統的網路架構。他也對未來5G的發展擔當著重要的腳色，5G遵循SDN「轉發、控制分離」這一基本原則，在設計5G網絡架構時做出重大改變：數據面下沉加上控制面集中。5G的SDN switch，能夠在流量導出與分流，移動邊緣計算，高可靠、低時延通信等業務中發揮重要作用。

通常SDN的架構是以Openflow標準通訊協定來控管底層的SDN router，Openflow是control plane跟data plane之間的協定。Openflow可以使網路管理員更自由地應用及管理其架構下的網路。

&nbsp;
### **Openflow主要有三個部分：**
---
- **Flow Table(流程表)：** 在交換器中寫入封包的流向，封包進入交換器後依照流程表所定義的流向來傳送封包<br>
- **Secure Channel(安全通道)：** 在流程表中沒定義其流向的封包會進入控制器，由控制器決定封包接下來的流向<br>
- **Openflow Protocol(Openflow通訊協定)：** 透過 SSL 加密通道，讓交換器以及控制器進行溝通

<center>

![](https://imgur.com/LnBYIql.jpg)<br>
**Figure：openflow內部與controller連接圖**
</center><p>

Switch工作於OSI7層中的第2層(data link)，switch內部的CPU會在每個port連接成功時，通過MAC Address和port對應，形成一張MAC表。在今後的該MAC Address的封包就送往他對應的port。簡而言之，switch就是分配封包該往哪裡送。傳統的switch就是從封包傳遞、網路管理、應用程式都是由自己一台機器所控制，其優點就是光靠硬體設計就可以完成將所有任務，缺點就是如果需要改變某些的設定已經寫入硬體，可能要直接更換一台switch。而SDN網路架構底層只負責封包傳遞，傳統switch的網路管理與應用程式都被移到controller上，由controller統一控制。優點就是可以迅速更改設定且不需更換switch，省下成本及人力。

<center>

![](https://imgur.com/TCTJKcO.jpg)<br>
**Figure：傳統網路與SDN網路比較圖**
</center>
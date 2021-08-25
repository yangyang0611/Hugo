---
title: "P4 17: Paper 論文"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/ARPsproof.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

## **TITLE**
<font color = #4F4F4F>

**| Firewall rule with token bucket as a DDoS protection tool**</font>

### **Abstract**
The paper says that most of the methods of DDoS protection are based on using firewall and IDS/IPS mechanisms to fight attacks are not sufficient enough. This paper the author presents a new method for counteracting DDoS - firewall rule with token bucket implementation from QoS method.

### **Enhanced QoS Method**
---
#### **1. Discription**
Tradition firewalls will only block the incoming traffic on specific ports or IP address ranges. This paper will present a new firewall method by limiting the incoming traffic on a firewall and allow servers to deal with already established connection.

#### **2. Firewall rule with token bucket**
The role of input firewall is to control the incoming traffic on the network edge. For example, on an HTTP server, usually the TCP port 80 has to be opened for incoming connections. This port is still open when an attack occurs. This is what leads to server overload. So a special firewall module is developed, the role of it is to filter the traffic and limit it according to the policy.

#### **Methods**
儅一堆封包進來，port依舊不會被關閉，方法如下：
1. 沒被攻擊 → 正常傳送packet，*packet_counter*++
2. 在time t，packet數量超過 *packet_limit*，啓動DDos攻擊
3. filter進來的IP address (*listIP*)
4. 如果是合法IP，傳給network；否則，檢查*packet_counter*是都超過*packet_limit*，超過就DROP
5. 同時，*packet_counter*數量歸0，restart filtration process 
6.  儅短時間内封包數量突然大增 (*some_limit*) 代表被攻擊，*packet_limit* 數量減半
7. 如果沒有遇到*some_limit*問題，*packet_limit*數量*2

**token bucket示意圖**：
![](https://imgur.com/9MnewOel.jpg)

#### *Pseodocode*
```python
packet_counter:=packet_counter + 1
if packet_counter < packet_limit then
    packet pass
else
    begin
        if IP address in listIP then
            packet pass;
        else
            packet drop;
    end;
if times_slots ends then
    begin
        if packet_counter>packet_limit then
            overdrop_times=overdrop_times + 1;
        packet_counter=0;
        if overdrop_times>some_limit then
            packet_limit=packet_limit/2;
            overdrop_times=0;
        else
            packet_limit=packet_limit*2;
            overdrop_times=0;
    end;
```

&nbsp;
## **TITLE**
<font color = #4F4F4F>

**| Developing of Algorithm of HTTP FLOOD DDoS Protection**</font>

### **Abstract**
保護user免受廣告干擾 和 提供改良版DDoS防禦措施

#### **http攻擊手法：**
1. 控制 user電腦（通過木馬、病毒、蟲），使其變成僵尸電腦，形成botent network（僵尸網路）
2. 同時向目標發送大量 http 封包，造成阻塞

<u>**Disadvantages：**</u>
- 流通別人家的 algorithm 秘密，company 不知道要買哪個（怕買到盜版）
- 購買昂貴DDoS protection service

![](https://imgur.com/MbMfh7zm.jpg)
![](https://imgur.com/ZGrPL5Bm.jpg)<br>
User request，先通過proxy server做處理，確認安全后response 給User，再連去target server

### **Proxy 使用**
1. Local network 裏的device 連去global network
2. 擁有cache，如果重複呼叫安全http，target server會快速回傳。
另，proxy靠近 user，如果更改資訊，可以更改 http header 就可以了，效率提升
3. 壓縮内容，減少traffic transmitted
4. 處理廣告，proxy作爲host直接access global network
5. proxy作爲代理host，隱藏了user的IP address，減少被攻擊

### **Proxy 分類**
---
#### **1. Transparent Proxy**
- User沒有權限直接access target server b，要經過server z
- router壞掉，要經過server z
![](https://imgur.com/m1UsIEVl.jpg)

#### **2. Reverse Proxy**
User通過server z 向target server尋求IP，但user並不知道z 的存在。

如果很多user同時request，server z 知道是安全IP立刻傳回adress給user（cache），不需要經過target server b → **balance network load**
![](https://imgur.com/F0bEwWil.jpg)

#### **3. Web Server**
也是作爲user連上target server的代理 server，匿名讀取

### **Blocking Algorithm**
![](https://imgur.com/KMy3oORl.jpg)
![](https://imgur.com/14ohtVUl.jpg)

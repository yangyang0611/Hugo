---
title: "P4 07: Control Plane with P4 Runtime"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/ARPsproof.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

這次的練習是試著使用p4runtime來實作control plane

使用的topology如下，3個switch分別有host，然後有一個tunnel連接h1 h2<br>
![](https://imgur.com/piG5DF0l.jpg)

要實作controller要先了解p4runtime_lib的一些東西<br>
所以先從helper.py開始看

<u>helper.py</u>
1. Contains the P4InfoHelper class. which is used to parse the p4info files.
2. Provides translation methods from entity name to and from ID number.
3. Builds P4 program-dependent sections of P4Runtime table entries.

p4info是一個將table action ID 都寫在裡面的檔案<br>
可以在執行make run指令後在build資料夾裡找到

下圖為p4info.txt
![](https://imgur.com/AgZ8KTBl.jpg)

helper.py裡面只有一個class 叫做 P4InfoHelper<br>
一開始的初始化(init)是將 p4info 檔案丟進一個空的 p4info 物件<br>
![](https://imgur.com/JrrXVWJl.jpg)

接下來的get函式會將 p4info 裡的 entity_type 丟進 o 這個變數 去尋找對應的名稱或ID<br>
![](https://imgur.com/wGavevtl.jpg)

get_id 會還傳self的ID<br>
get_name會回傳self的name<br>
get_alias會回傳self的alias<br>
![](https://imgur.com/783KiCKl.jpg)

getattr就是將 id 搜尋的函式與 name 搜尋函式合成<br>
![](https://imgur.com/UQprW2el.jpg)

get match field 就是在 p4info.helper 裡的 table 搜尋所提供的 name 或 ID<br>
![](https://imgur.com/QBayByPl.jpg)

get match field id 就是搜尋對應的ID<br>
get match field name 就是搜尋對應的name<br>
get match field pb 就是去找到對應的p4runtime_pb2<br>
![](https://imgur.com/CaT8l3Ul.jpg)
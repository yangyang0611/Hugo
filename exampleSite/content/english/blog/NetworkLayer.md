---
title: "Network Layer 網路層"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/network_layer.jpg"
tags: ["internet"]
description: "This is meta description."
draft: false
---

## **OverView Of Network Layer**
---
**control plane:** SDN 在這裏做事<br>
**data plane:** 單純資料傳輸

&nbsp;
## **What is inside a router?**
---
![](https://imgur.com/uBWRks9l.jpg)
- **Destination Based Forwarding：** 根據 dest IP 來傳資料 （traditional)<br>
- **Generalize Forwarding：** 根據自定義的 header IP 來傳資料

&nbsp;
#### **lmp(Longest Prefix Match)**
對進來的 IP 做查表，數字對應最多的就是 destination address
![](https://imgur.com/p5T6hjQl.jpg)<br>
**Example：** Which interface is <br>
DA: 11001000  00010111  0001**0110  10100001**?<br>
A: interface 0

DA: 11001000  00010111  0001**1000  10101010**?<br>
A: interface 1

&nbsp;
#### **Head of Line Blocking**
前面的 package 還沒出去，阻擋了下一個 packet 的傳輸<br>
![](https://imgur.com/V9UosWYl.jpg)

**Q：我們如何得知自己的 subweb mask?**<br>
A：從ISR (Internet Service Provider) 那裏得到

**Q：ISP 如何得到 block of address 的？**<br>
A：從ICANN（Internet Corporation for Assigned Names and Number<br>
eg: https://www.fb.com

- DNS
- domain name
- allocated address

&nbsp;
#### **CDIR**
**8 bits. 8 bits. 7 bits. 9 bits / 23 bits subnet part**

*也有 IP address 是 220.23.16.0/24 ， subnet mark 是 24 bits 咯
![](https://imgur.com/wNw0jLTl.jpg)

&nbsp;
#### **Hierarchical Addressing**
把 domain name 轉換成 ip address
![](https://imgur.com/vCdPMoRl.jpg)

&nbsp;
#### **IPv6 Tunneling**
**IPv6 的 header 裏包裝一部分 IPv4 的header，因此 Tunneling 執行時 中間那段是IPv4 的 Tunneling**
(暫時，未來將會全面被 IPv6 header 取代)
![](https://imgur.com/0gXeYlcl.jpg)

&nbsp;
#### **Network Address Translation(NAT)**
上網一定要通過 public IP address，但假如每個 device 都有public IP，世界上的 IP 就會用完。
因此，一個家裏的所有 device 就有自己的 private IP，上網時，通過 NAT （private —> public）
回傳時（public —> private）
*目前已有 IPv6 解決 IP 分配不足問題
![](https://imgur.com/wpTgf0El.jpg)

&nbsp;
## **Overflow Abstraction**
---
##### <u>**Firewall**</u>
- match: IP address, TCP/UDP header
- action: sent / block

##### <u>**NAT**</u>
- match: IP address
- action: rewrite port & address

##### <u>**Switch**</u>
- match: MAC address
- action: forward & flood

##### <u>**Router**</u>
- match: lmp
- action: forwarding
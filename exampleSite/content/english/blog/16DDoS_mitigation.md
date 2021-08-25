---
title: "P4 16: DDoS Mitigation"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/ddos_mitigation.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

## **What is DDoS Mitigation?**
---
DDOS Mitigation 是一個用來抵抗或降低DDOS攻擊對伺服器影響的工具
第一步是透過定義 traffic pattern 來辨識網路流量的正常情況，偵測DDOS有沒有發生

<font color=#4F4F4F>

**| Traffic Pattern is a part of the    totally connected network trafiic. It represents the traffic between two networks : Internal and External network.**</font>


之後還需要辨識進來的traffic把正常人們用的流量跟機器人或是爬蟲區分開來。這一步是透過比對signature 或是檢查traffic attributes 像是 IP 位址, cookies, HTTP headers 之類

接下來就是 filtering，filtering 可以過以下的技術來達到：
- connection tracking
- IP reputation lists
- deep packet inspection
- blacklisting/whitelisting
- rate limiting

### Connection Tracking
We use connection tracking to track information about traffic to and from the instance. Rules are applied based on the connection state of the traffic to determine if the traffic is allowed or denied.

### IP Reputaion Lists
IP reputation is a tool that identifies IP addresses that send unwanted requests. Using the IP reputation list you can reject requests that are coming from an IP address with a bad reputation.

### Deep Packet Inspection
DPI is a type of data processing that inspects in detail the data being sent over a computer network. Deep packet inspection is often used to baseline application behavior, analyze network usage, troubleshoot network performance, ensure that data is in the correct format.

### Blacklisting/Whitelisting
The blacklisting approach involves defining which entities should be blocked. A blacklist is a list of suspicious or malicious entities that should be denied access or running rights on a network or system. Instead of creating a list of threats, whitelisting creates a list of permitted entities and block everything else.

### Rate Limiting
Rate limiting is a strategy for limiting network traffic. It puts a cap on how often someone can repeat an action within a certain timeframe – for instance, trying to log in to an account.
---
title: "File Transfer on UDP TCP"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/file_transfer.jpg"
categories: ["internet"]
description: "This is meta description."
draft: false
project_info:
- name: "Completer"
  icon: "fas fa-user"
  content: "Yi-Ting Yang"
- name: "Project Link"
  icon: "fas fa-link"
  content: "https://github.com/yangyang0611/File-Transfer-on-TCP-UDP"
- name: "Demo Video"
  icon: "fas fa-video"
  content: ""
---

**NOTICE: CLIENT'S WINDOWS SHOULD BE OPEN BEFORE SERVER'S WINDOW**

## **Project Details**

&nbsp;
### **Lab 1**
#### 'Implimentation package transfering on TCP & UDP protocol'

&nbsp;
##### **A. server --- send document**<br>
**<u>command line:**</u><br>
gcc –o server <程式碼檔名> <br>
./server <tcp/udp> send <ip addr> <port> <.txt>

- divided document into serveral socket
- print out succeed transfering time with every 25% send
- print out total transition time
- print out file size

<center>

![](https://imgur.com/DGFRRdIl.jpg)<br>
**Figure:TCP server**

![](https://imgur.com/B4OVYd5l.jpg)<br>
**Figure:UDP server**
</center>

##### **B. client --- receive document**
**<u>command line:**</u><br>
gcc –o client <程式碼檔名> <br>
./client <tcp/udp> recv <ip addr> <port>

- print out total packet received (in UDP protocol)
- print out packet lost (in UDP protocol)
- create a new file when transfer is succed

<center>

![](https://imgur.com/fpjK7R0l.jpg)<br>
**Figure:TCP client**

![](https://imgur.com/CJnOSmTl.jpg)<br>
**Figure:UDP client**
</center>

&nbsp;
## **Lab 2**
#### 'LLMP multicast -- which can only be implemented on UDP protocol'

&nbsp;
##### **A. server --- send document to 3 client**
<u>**command line:**</u><br>
gcc –o s <程式碼檔名><br>
./s server multicast <txt檔名>
- print out file size TO BE SEND
- show when file was sent successfully
<center>

![](https://imgur.com/kX6O3gbl.jpg)
**Figure:UDP server**
</center>

##### **B. 3 client --- receive document from a server**
<u>**command line:**</u><br>
gcc –o c <程式碼檔名><br>
./c client multicast
- each print out received file size (may be vary)

<center>

![](https://imgur.com/1f9MOool.jpg)<br>
**Figure: Client 1**

![](https://imgur.com/pXCNS5vl.jpg)<br>
**Figure: Client 2**

![](https://imgur.com/6a7Tb5hl.jpg)<br>
**Figure: Client 3**
</center>

&nbsp;
### **Lab 3**
#### 'Analysis & Trobleshoot with WireShark -- an open-source package analyser'

&nbsp;
##### **Q1: How to know MAC Address and IP Address?**

Ans: In command prompt, enter:'ipconfig/all'.<br>
![](https://imgur.com/9diXzPel.jpg)

&nbsp;
##### **Q2: How to know the computer is connected to the internet?**

Ans: In command prompt, enter: 'ping<internet_ip_addr>'<br>
If server return data byte, time, TTL, send, receive, lost packages, and ect messages will be a prove of succeed connection.<br>
![](https://imgur.com/4W8bv4Dl.jpg)

&nbsp;
##### **Q3: The speed of a web page loading is abnormally slow. How to find out the node of performance bottleneck without considering the performance of local computer and web server?**

Ans: In command prompt, enter: 'tracert <internet_ip_addr>'<br>
This will show the path the packet took to reach the target host, and
and shows the time to each node, i.e., how to get to where you want to go.<br>
![](https://imgur.com/LJLi7SPl.jpg)

&nbsp;
##### **Q4: How can I observe which ports are open on my computer?**

Ans: In command prompt, enter: 'netstat -na'.(Or 'netstat')<br>
LISTENING indicating that the local machine is listening on port 808 and waiting for the remote computer to connect (i.e., it is the open state)
![](https://imgur.com/vQD7JiZl.jpg)

&nbsp;
##### **Q5: How to find IP Address of 'www.facebook.com'?**

Ans: In command prompt, enter: 'nalookup www.facebook.com'.<br>
![](https://imgur.com/11BaA8Xl.jpg)

&nbsp;
##### **Q6: Connect to http://www.facebook.com.tw. Show how to get <u>HTTP GET</u> and <u>respond message.</u>**

Ans: 
HTTP GET & Respond:<br>
![](https://imgur.com/e9UeaREl.jpg)

HTTP GET:<br>
![](https://imgur.com/Jwh1X1Rl.jpg)

Respond:<br>
![](https://imgur.com/sKTUdPHl.jpg)

&nbsp;
##### **Q7: Connect to http://www.facebook.com.tw. Is HTTP respond is 200 OK or 304 Not modified? If not, explain why.**

Ans: No. The HyperText Transfer Protocol (HTTP) 302 Found redirect status response code indicates that the resource requested has been temporarily moved to the URL given by the Location header. A browser redirects to this page but search engines don't update their links to the resource (in 'SEO-speak', it is said that the 'link-juice' is not sent to the new URL). <br>
![](https://imgur.com/DuJeMW3l.jpg)
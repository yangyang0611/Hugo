---
title: "Socket"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/socket.jpg"
tags: ["internet"]
description: "This is meta description."
draft: false
---

## **What is Socket?**
---
Socket，中文叫做端口。儅使用者（client)想要鏈接互聯網時，便會吧自己的ip以及macAddr放到這個端口上。同時，server也會在Socket的另一端。兩台機器處於同一條internet line上的兩端，便可以開始通信。這時就可以使用不同的同行協議來完成訊息傳輸。
 
&nbsp;
## **TCP Flow**
![](https://imgur.com/xcMTNrB.jpg)

&nbsp;
## **UDP Flow**
![](https://imgur.com/VjtsFSL.jpg)

&nbsp;
## **Structure**
---
### **Socket()**
```python
#include <sys/types.h> /* See NOTES */
#include <sys/socket.h>

int socket(int domain, int type, int protocol);
```

##### **domain:**
- **AF_INET：** 產生socket協議，用TCP/UDP傳輸，ipv4 address
- **AP_INET6：** 跟上面一樣，用Ipv4 address
- **AF_UNIX`：** 本地協議，在UNIX & LINUX系統上使用（user and server 在同台）

##### **type:**
- **SOCK_STREAM：** 按順序，可靠的TCP傳輸
- **SOCK_DGRAM：** 固定長度傳輸，不可靠的UDP

##### **protocol:**
0 默認協議

### **bind()**
```python
int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
```
`成功return 0， else return -1`<br>
server監聽的網路地址 & port 固定（eg：http port80）。因此，儅client得知server的address和port之後就可以向server請求internet connection。每台server有固定port number 和ip address。<br>
得知addr后便能把sockdf文件傳去指定Ip & port
- **sockdf:** socket 文件描述相符<br>
- **addr:** 構造ip addr & port<br>
- **addrlen:** sizeof(addr)

### **listen()**
```python
int listen(int sockfd, int backlog);
```

`成功return 0, 失敗 return -1`<br>
有request 就呼叫accept()確認連接。如果request太多，user的sockdf處於listen()狀態，最多允許backlog個user等待，超過就ignore
- **backlog:** handshaking 3次

### **accept()**
```python
int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
```

`成功return new sockfd，失敗 return -1`<br>
handshaking后，發動accept()，if no user connection, then wait until there is
- **addr:** addr 傳NULL，代表不 care user address
- **addrlen:** 傳入user提供的buffer addr 長度（overflow處理），傳出user address實際長度（maybe 滅有占滿user provided 的buffer length）

### **connection()**
```python
int connect(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
```
`成功return 0， 失敗-1`<br>
呼叫connect()，連接server<br>
**與bind()差別，bind() addr是自己地址，connect()是對反地址**

### **read()**
```python
int my_read(int fd,void *buffer,int length)
```
read from fd , store in buffer<br>
user define buffer max length : n

### write()
```python
int my_write(int fd,void *buffer,int length)
```
read from buffer, store in fd

![](https://imgur.com/A4fR73G.jpg)<br>
**Figure: client連接互聯網的流程圖**

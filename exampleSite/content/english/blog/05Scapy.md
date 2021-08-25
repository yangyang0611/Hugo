---
title: "P4 05: Scapy"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/ARPsproof.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

## **What is Scapy?**
---
在P4教學裡面使用python寫的資料都include了scapy這個library，scapy是用python寫成的，是一個用來處理封包的工具，還可以掃描、跟蹤路由、探測、單元測試、攻擊和網絡發現等。

簡單的scapy使用 :
```c#
data='hello,word!'
pkt=IP(src='10.96.10.208',dst='10.96.10.209')/TCP(sport=12345,dport=12345)/data
send(pkt,inter=1,count=5)
```
格式是 : 第三層協議(參數)/第四層協議(參數)<br>
Inter是間隔幾秒發送一次封包<br>
Count是一次要發送幾個封包<br>
![](https://imgur.com/babirZfl.jpg)<br>
<font color=#00800>
**封包發送成功**</font>

在send.py裡使用到<br>
也可以透過ethernet發送封包<br>
```python
def sendp(x, inter=0, loop=0, iface=None, iface_hint=None, count=None, verbose=None, realtime=None,
          return_packets=False, socket=None，*args,**kargs)
```

iface是一個變數操控ifup跟ifdown 操控網路介面開啟跟關閉<br>
verbose是要不要將執行的指令顯示<br>
![](https://imgur.com/71y7Eikl.jpg)<br>
<font color=#00800>
**send.py使用到的範例**</font>

scapy抓封包是使用sniff<br>
```python
def sniff(count=0, store=1, offline=None, prn=None,filter=None, L2socket=None, timeout=None, opened_socket=None, stop_filter=None, iface=None，*args,**kargs)
```
![](https://imgur.com/wZtJ5q2l.jpg)
<font color=#00800>
**receive.py使用到的範例**</font>

可以將剛剛用sniff所抓取的封包儲存
```python
package=sniff(iface='eth0',count=10)
package = sniff(offline='test.pcap')
```

再將儲存起來的封包顯示出來
```python
wrpcap("test.pcap",package)   #儲存剛剛所抓的封包為test.pcap
	print(package)
Sniffed: TCP:0 UDP:10 ICMP:0 Other:0>
```
從上方的output可以看到抓到了10個UDP的封包<br>
透過package[i] 可以檢視第i個封包

```python
print(package[0])   
print(package[0].show())
```
過濾封包是使用filter，filter 使用的是 Berkeley Packet Filter (BPF)語法，也是wireshark使用的過濾語法<br>
例如我們只要抓icmp的封包，就是在filter後加上icmp

```python
sniff(filter="icmp",count=5,prn=lambda x : x.sprintf("{IP:%IP.src%-> %IP.dst%}"))
```
BPF是類unix系統上data link layer的一個interface，提供data link layer封包的收發。<br>
他的過濾功能以BPF的虛擬機的機器語言的直譯器的方式實現的，使用這種語言寫的程式可以抓取封包，對封包中的資料進行運算，並將數據包中的資料和結果中的資料做比較，根據比較的結果決定接受還是拒絕封包。

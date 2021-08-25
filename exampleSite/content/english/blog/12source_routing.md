---
title: "P4 12: Source Routing"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/ARPsproof.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

## **What is Source Routing?**
通過輸入一串port的編號來決定封包傳送的方向

使用的topology如下：
![](https://imgur.com/3AsArEll.jpg)

sourcerouting.p4 需要以下的元件:
1. 宣告 ethernet, ipv4 和 source route 的 header
2. Parse ethernet, ipv4 , source route
3. 一個 action 來丟棄封包 **mark_to_drop()**
4. 一個 action **srcRoute_nhop** 來設定下一個hop的egress port 和移除第一個 srcRoute 的 entry
5. 一個 control **apply** 確定接下來 source route 存在, 如果是最後一個 hop 就更改 etherent.etherType, 呼叫**srcRoute_nhop**
6. deparser
7. package

首先新增一個 srcRoute_t 的 header
```python
header srcRoute_t {
    bit<1>    bos;
    bit<15>   port;
}
```
這是用來存port的編號跟是不是stack裡的最後一個

之後在parse ethernet的時候 如果他的etherType 是 TYPE_SRCROUTING 就要去parse srcRouting
```python
state parse_ethernet {
        packet.extract(hdr.ethernet);
        transition select(hdr.ethernet.etherType) {
            TYPE_SRCROUTING: parse_srcRouting;
            default: accept;
        }
    }
```

在 parse_srcRouting 要寫好如果bos是0 就要parse下一個entry
```python
state parse_srcRouting {
        packet.extract(hdr.srcRoutes.next);
        transition select(hdr.srcRoutes.last.bos) {
            1: parse_ipv4;
            default: parse_srcRouting;
        }
    }
```

接下要定義 **src_nhop()** 要將egress spec 設定成 srcRoute[0] 然後pop掉
```python
action srcRoute_nhop() {
        standard_metadata.egress_spec = (bit<9>)hdr.srcRoutes[0].port;
        hdr.srcRoutes.pop_front(1);
    }
```

再來就是要完成 MyIngress 這個的 control<br>
如果port stack是空的(bos==1) 就要finish 然後要把ethertype 改成 ip<br>
如果不是空的就要執行 **srcRoute_nhop()**

我們就可以透過 **./send.py 10.0.0.2**<br>
然後輸入一串數字 **2 3 2 2 1** 代表我們的路徑是經過h1 s1 s2 s3 s1 s2 到 h2
![](https://imgur.com/fM8xhd5.jpg)<br>
<font color="#00800">
**傳送封包**</font>

![](https://imgur.com/3SEIsm4.jpg)<br>
<font color="#00800">
**h2成功收到封包**</font>

輸入一串數字當作port是被定義在 send.py裡面
```python
print
s = str(raw_input('Type space seperated port nums '(example: "2 3 2 2 1")' or "q" to quit: '))

if s == "q":
    break;
```
```python
for p in s.split(" "):
    try:
        pkt = pkt / SourceRoute(bos=0， port=int(p))
        i = i + 1
    except ValueError:
        pass
if pkt.haslayer(SourceRoute):
    pkt.gerlayer(SourceRoute, i).bos = 1
```

會將輸入的 s 字串分成一個一個依序加入**SourceRoute**的port裡
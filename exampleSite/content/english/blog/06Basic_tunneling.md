---
title: "P4 06: Basic Tunneling"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/ARPsproof.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

## **What is Basic Tunneling?**
---
使用basic tunneling是可以將不同protocol下的封包在不更改protocol情況下往前傳送

使用的拓樸如下：
![](https://imgur.com/AfKlEjOl.jpg)

&nbsp;
### **Basic Tunneling 實作**
---
在exercises/basic_tunneling 裡面輸入**make run** 建立mininet<br>
在分別使用xterm開出host1跟host2 **xterm h1 h2**

之後在h2 輸入 **./receive.py** 來接收等等的封包<br>
首先測試看看一般不使用tunneling下封包的傳送<br>
在h1輸入 **./send.py 10.0.2.2 “hi I am steven”**<br>
![](https://imgur.com/JwIEVEbl.jpg)
<font color=#00800>
**看到h2有成功收到封包 有ethernet TCP IP的header**</font>

接下來使用tunneling<br>
在h1輸入**./send.py 10.0.2.2 “hi I am steven” –dst_id 2**<br>
![](https://imgur.com/Ywg1QK2l.jpg)<br>
<font color=#00800>

**h2收到的封包會多一個tunnel的header**
</font>

此時如果試試看使用tunnel但是把destination ip 設為h3<br>
h1輸入 **./send.py 10.0.3.3 “hi I am steven” –dst_id 2**<br>
![](https://imgur.com/tyCeiBIl.jpg)<br>
<font color=#00800>
**還是在h2被收到，原因是switch在有tunnel header的情況下並不會使用ip來routing**</font>

&nbsp;
## **run_excercise.py**
---
從main開始看

先進去**args=get_args()**
![](https://imgur.com/2m2YBRgl.jpg)
<font color=#00800>
**get_args()大概就是在處理一開始輸入的arguments**</font>

接下來執行到的是下面這行指令：
```python
exercise = ExerciseRunner(args.topo, args.log_dir, args.pcap_dir, args.switch_json, args.behavioral_exe, args.quiet)
```
之後在main執行到的是 **exercise.run_exercise()**<br>
![](https://imgur.com/EmyqZ11l.jpg)
<font color=#00800>
**建立ExerciseRunner這個物件時，init會將許多參數與變數設定好與讀取 topology.json**</font>

ExerciseRunner 的 **run_exercise()** 大致上就是建立mininet<br>
Create_network()
![](https://imgur.com/nOW8KfVl.jpg)
<font color=#00800>
**建立mininet網路然後將它存在self.net這個變數裡**</font>

其中 ConfigureP4Switch()<br>
![](https://imgur.com/YiRWLncl.jpg)
<font color=#00800>
**確認每個switch的thrift server都使用獨立的port<br>
使用到從p4runtime_switch import 來的 P4RuntimeSwitch class**<br>
</font>

#### **Thrift**
被當作RPC框架使用，可以定義一個服務或改變通訊和傳輸協議，而無需重新編譯code。

#### **RPC**
remote procedure control該協定允許執行於一台電腦的程式呼叫另一個位址空間的子程式

#### **ExerciseTopo()**
p4 tutorial exercise裡面的topology class，設定好topology<br>
回到一開始的run_exercise()

#### **Program_hosts()**
在每個host下執行topology.json裡面的指令

#### **Self.do_net_CLI()**
建立mininet CLI，並且output一些有用的訊息
![](https://imgur.com/cvIIiKpl.jpg)
<font color=#00800>
**每次make run看到的成功訊息便是在Self.do_net_CLI()裡面print的**
</font>
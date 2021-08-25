---
title: "P4 08: Controller 實作"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/ARPsproof.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

從mycontroller.py裡的main開始看<br>
![](https://imgur.com/RyLpaD3l.jpg)

把switch1 跟 switch2 的data dump到給定的txt檔
```python
s1.MasterArtitrationUpdata()
s2.MasterArtitrationUpdata()
```

傳送master arbitration來設定這個controller為master<br>
可以去utils/p4runtime_lib/switch.py找定義
![](https://imgur.com/Ff0pBqkl.jpg)

<span style="background-color:lightgray">request=p4runtime_pb2.StreamMessageRequest</span><br>
在 p4lang/p4runtime/blob/master/proto/p4/v1/p4runtime.proto 可以看到定義<br>
![](https://imgur.com/5W0Kn0El.jpg)

oneof 的用法是只有一個在update裡的資料會被改動<br>
![](https://imgur.com/Xwm8elvl.jpg)

<span style="background-color:lightgray">
request.arbitration.device_id=self.device.id</span><br>
設定目前要被arbitrate的client

&nbsp;
## 
![](https://imgur.com/eeE464F.jpg)<br>
這幾行是在安裝p4 program到每個switch上<br>
<span style="background-color:lightgray">SetForwardingPipelineConfig()</span>可以在switch.py找定義
![](https://imgur.com/AIaY8fL.jpg)

去p4runtime.proto找 
<span style="background-color:lightgray">SetFowardingPipelineConfigRequest()</span><br>
![](https://imgur.com/EhEWNTR.jpg)<br>
可以看到是在定義每個action代表的動作

&nbsp;
##
![](https://imgur.com/svjJU5dl.jpg)<br>
把tunnel的traffic rules寫進去<br>
<span style="background-color:lightgray">writeTunnelRules()</span>可以在mycontroller.py上面一點找到<br>
<span style="background-color:lightgray">writeTunnelRules()</span>是在做3件事:
1. **tunnel ingress rule:** encapsulates traffic into a tunnel with the specified ID
2. **tunnel transit rule:** forwards traffic based on the specified ID
3. **tunnel egress rule:** decapsulates traffic with the specified ID and sends it to the host
```python
readTableRules(p4info_helper, s1)
readTableRules(p4info_helper, s2)
```

&nbsp;
##
從switch1 跟 switch2 讀取table entry
![](https://imgur.com/C1a6aCcl.jpg)<br>
更詳細的在report 07

&nbsp;

![](https://imgur.com/BDNxtTpl.jpg)

&nbsp;

每兩秒印出tunnel counters<br>
![](https://imgur.com/TGd5NvOl.jpg)

<span style="background-color:lightgrey">sw.ReadCounters()</span>可以在p4runtime_lib/switch.py裡找到<br>
![](https://imgur.com/9GyuLY1l.jpg)

<span style="background-color:lightgrey">ReadRequest()</span>在p4runtime.proto可以找到<br>
![](https://imgur.com/v3vY1fNl.jpg)<br>
Entity 可以從p4runtime.proto上方找到<br>
![](https://imgur.com/njoLhE2l.jpg)

可以看到我們設定entities為2 就是要讀table entry<br>
`yield`是在迴圈裡遇到這行statement便會暫停跳出去<br>
p4runtime_pb2 找不到<br>
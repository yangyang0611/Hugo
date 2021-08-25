---
title: "P4 14: Runtime Controller"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/ARPsproof.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

自己寫的 controller 要把 table entries 那些裝在 switch 上
controller 的流程圖大概如下<br>
![](https://imgur.com/OmGhOGE.jpg)

接下來會從每個state開始說明

首先會將一個 p4infohelper 這個物件創立出來<br>
<font color=#800000>
p4info_helper = p4runtime_lib.helper.P4InfoHelper(p4info_file_path)</font><br>
這個的目的是為了更好操作我們的table entry, p4info_helper 有很多function 可以呼叫

&nbsp;
### **Create Switch Connections**
我們會將一個switch 建立好
```python
s1 = p4runtime_lib.bmv2.Bmv2SwitchConnection(
            name='s1',
            address='127.0.0.1:50051',
            device_id=0,
            proto_dump_file='logs/s1-p4runtime-requests.txt')
```

我們可以看到是使用 bmv2 的 switch 然後會將資料丟到 logs 這個資料夾裡<br>
<font color=#008000>
**---> 可以去utils/p4runtime_lib/helper.py找定義**
</font>

&nbsp;
### **Send Master Arbitration**
建立完成後就可以傳送 arbritration 來宣告這個 controller 是 master<br>
<font color=#800000>s1.MasterArbitrationUpdate()</font><br>
<font color=#008000>
**---> 可以去utils/p4runtime_lib/switch.py找定義**
</font>

&nbsp;
### **Install P4 Program**
設定好 master 後就可以安裝 p4 program 上去了

```python
s1.SetForwardingPipelineConfig(p4info=p4info_helper.p4info,
                                        bmv2_json_file_path=bmv2_file_path)
```
<font color=#008000>**---> 詳細解釋可以去看 Report 08**
</font>

&nbsp;
### **Write Tunnel Rules**
之後就是將 tunnel 建立好，兩個方向都要考慮到

```python
 writeTunnelRules(p4info_helper, ingress_sw=s1, egress_sw=s2, tunnel_id=100,
                    dst_eth_addr="08:00:00:00:02:22", dst_ip_addr="10.0.2.2")
```
這樣可以將 h1 連接到 h2
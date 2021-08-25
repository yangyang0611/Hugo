---
title: "P4 04: Introduction of P4"
date: 2020-05-12T12:14:34+06:00
image: "images/portfolio/blog/title/header_parser.jpg"
tags: ["Internet","Security","P4"]
description: "This is meta description."
draft: false
---

## **Introduction of P4**
---
**P4 主要用途：用戶自定義封包格式**<br>
以往使用者都是用定義好的ethernet_type，定義好的header，要更改格式就要換掉硬體設備，現在只要用p4定義，編輯器弄成硬體語言（FPGA / ARM binary），完放去switch，就ok

&nbsp;
## **v1model架構**
---
P4常使用到一個架構叫v1model<br>
而v1model standard metadata大概為這幾項:
```python
ingress_port: 封包抵達的port
egress_spec: 封包要被送往的port
egress_port: 封包要從哪個port被送出去

clone_spec , instance_type, drop, recirculate_port, packet_length, enq_timestamp, enq_qdepth, deq_timedelta, deq_qdepth, ingress_global_timesptamp, lf_field_list, mcast_grp, resubmit_flag, egress_field, checksum_error
```

P4教學裡使用的switch是 Bmv2 ( behavioral model version 2 )<br>
這個switch是由c++ 11 寫成的，bvm2並不是一個生產力導向的switch(像是ovswitch)，而是一個偏向開發使用的switch，測試和debug p4 的data plane。

P4中有5個語言組件
- header
- parser
- table
- action
- control

&nbsp;
### **Header**
Example: Ethernet header
``` python
header_type ethernet_t {
	field {
		dst_addr : 48;
		src_addr : 48;
		ether_addr : 16;
		}
}
```
可以定義其他的，如ipv4 ipv6等等，檔案放在header.p4，include到main裏<br>
要用時候寫 header ethernet_t ethernet;

&nbsp;
### **Parser**
``` python
parser start {
	return parser_ethernet;
}

parser parser_ethernet {
	extract (ethernet);
	return select(latest.ether_type) {
		0x0800 : parse_ipv4;
		default : ingress;
	}
}

parser parser_ethernet {
	extract (ethernet);
	return select(latest.ether_type) {
		0x0800 : parse_ipv4;
		default : ingress;
	}
}
```
- **Extract：** 把package 的header 取出來
- **Return：** 看要前往哪個parser / control function，可以直接return / select
- **Select (select_exp):** 像c 語言的switch case，根據不同field決定哪個Parser / control field
- **Select_exp：**
    1. **Latest.field_name：** 以最後extract的header爲主，用他的field
    2. **Current (offset, length)：** 以目前package offset開始，取length個長度的值
    3. **Field_ref：** 如ethernet.ether_type
        注：parser也可以return exception

&nbsp;
### **Action**
類似function
```python
action action_name ( param1, param2…) {
}
```

&nbsp;
### **Table**
像class， 每個entry就像table格式的object
```python
table table_name {
	reads { // 所有flow entry 的match type格式長這樣
		field1 : match_type1;
		field2 : match_field2;
	}
	actions { // flow entry action不一定都要執行
		action1;
	  action2;
	}
	size = 
	action = 
}
```
- Min_size : value; // table entry最小值，低過會error
- Max_size : value; // table entry最大值，超過會error
- Size : value; // 特定entry下做事
- Support_timeout : true or false; // 決定table接受entry時，是否會自動timeout掉
- Match_type
    1. Exact : 與match完全相同的match
    2. Lmp: longest prefix match, IP match eg: 140.113.0.0/16
    3. Valid: header file 又被parse出來就是valid

&nbsp;
### **Control**
Control program 控制一切，看看package要經過什麽table

Modify_field(standard_metadata.egress_spec,1)<br>
在metadata階段，讀取egress_spec的值，看要做什麽事

```python
Control control_function_name{
}
```

1. Apply(table name);<br>
    根據table裏的entry去apply相對動作

2. 
```python
apply(check_dmac){
	Ipv4_route {
		apply(ipv4_rpf);
		apply(ipv4_acl);
	}
default: {
	apply(ipv6_rpf);
	apply(ipv6_acl);
	}
}
```
根據table選到的action去決定apply哪一段control block。<br>
沒有列出就選default。

3. 
```python
if(valid(vlan))
	apply(vlan);
else
	my_metadate.vlan = 0;
```
- valid(heafer_ref) ：小時該header是合法的輸入/輸出
- eth.type == 0x0800 / ipv4.mask == 65535 基本布林運算

注：ingress完成會送到queue，但action呼叫resubmit / recirculate，送回ingression處理；呼叫clone_e2i則是複製一份封包，送去指定地點

&nbsp;
### **Standard Metadata**
每個package進來，自動產生好package的基礎元素，如ingress post, length等


---
title: "DDoS Defense Implement on P4"
date: 2021-06-30T12:14:34+06:00
image: "images/portfolio/DDoS.jpg"
categories: ["internet","security"]
description: "This is meta description."
draft: false
project_info:
- name: "Collaboration"
  icon: "fas fa-user"
  content: "Done in a group of 3"
- name: "Project Link"
  icon: "fas fa-link"
  content: "https://github.com/yangyang0611/DDoS-Defense-Inplement-on-p4"
- name: "Report"
  icon: "fas fa-file"
  content: "https://drive.google.com/file/d/1qo5FBpP4cdwunNihAW2OBcbaMvHMYbVL/view?usp=sharing"
- name: "Demo Video"
  icon: "fas fa-video"
  content: "https://drive.google.com/file/d/1LrCeo3VMdPP9FBnvQtl9n7ovNCdrDnhX/view?usp=sharing"
---

<b>DDoS(Distributed Denial of Service)</b> is a network attack technique that aims at exhausting the network or system resources of the target computer, temporarily disrupting or stopping the service and making it inaccessible to normal users. In recent years, due to the increase of IoT products, attackers can easily build huge botnets to generate huge amount of DDoS attacks, and studies show that a total of 400,000 DDoS attacks occur every month. However, DDoS defense has not kept up with the rapid development of DDoS attacks. The most commonly used defense mechanism today is the traffic cleansing center, but the equipment used to set up the traffic cleansing service center is inexpensive and not easy to maintain. Although these hardware devices are very efficient in processing packets, they are relatively inflexible in terms of capacity, functionality, and location. When new attacks emerge, the hardware has to be upgraded, so there is a significant financial expense.
 
SDN is a network design concept that lies on the datalink layer and network layer. Application Layer, Control Layer, and Infrastructure Layer, which separates the control plane (routing, ARP, DHCP) and data plane (IPv4, IPv6) of router to the controller. SDN has three major advantages: cost reduction, efficiency, security and stability. The SDN network architecture takes less time to configure than traditional networks when upgrading. 

Today, SDN can program the data plane through programmable swtich and domain-specific language. The most popular language in the domain-specific language is P4, which is known as Programming Protocol Independent Packet Processors, and allows us to programmatically define the behavior of each packet to make the access and operation of packets more efficient. P4 allows us to programmatically define the behavior of each packet, making packet access and operation more efficient. 

#### **Project Details**
The first step is to select the type of defense to be implemented, then define the topology, and use scapy and python to test the completed defense mechanism separately. Because Openflow is often used nowadays, the switch itself does not know the topology, so we added LLDP to let the controller know the connection status of each node. Finally, all the mechanisms are integrated and tested together. 

Our selection of DDoS attacks are:
- SYN Flood
- SYN-ACK Flood
- DNS Amplification
- ICMP Flood

![](https://imgur.com/KyIYZg2l.jpg)

#### **Project Archeivement**
##### **[Normally]**<br>
Maximum number of packages lies between 400-500<br>
![](https://imgur.com/N6DZJ2Kl.jpg)

##### **[DDoS Attack without firewall]**<br>
Number of packages lies between 150<br>
![](https://imgur.com/iOPeLILl.jpg)

##### **[DDoS Attack with firewall]**<br>
The normal packets were only about 150 when the attack was originally launched. It is now back to normal when firewall is turned as abnormal IP traffic is restricted. 

Finally, we adjust the limit value in the P4 program to compare the packet traffic status

**1. Set Limit = 10**
![](https://imgur.com/pXI2zzql.jpg)

**2. Set Limit = 100**
![](https://imgur.com/Czxa15Cl.jpg)

When the defense is on, switch will determine whether the number of packets sent by this IP has exceeded a value (limit). Because DDoS attack will cause a large number of packets to fill the host and occupy the resources, it restricted the abnormal IP flow, only the packets to those that are not attacks can go through.**This is the core concept of our defense mechanism.**

If you adjust the limit to a larger value, the number of packets passing through the switch defense will increase, and you will not be able to intercept the attacking packets.

If the limit is set too small, it cause fewer packets to pass through, limiting the packets to those that are not attacks. So it is important to set the limit to an optimal value.
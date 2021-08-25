---
title: "Doodle Jump"
date: 2021-07-30T12:14:34+06:00
image: "images/portfolio/doodle_jump.jpg"
categories: ["design","development"]
description: "This is meta description."
draft: false
project_info:
- name: "Completer"
  icon: "fas fa-user"
  content: "Yi-Ting Yang"
- name: "Project Link"
  icon: "fas fa-link"
  content: "https://github.com/yangyang0611/DoodleJump-QT"
- name: "Demo Link"
  icon: "fas fa-video"
  content: ""
---

這是一款解壓小游戲，名叫Doodle Jump。

## **Project Details**
1. 按下start button, 玩家可以用两个方向（左右）移动Doodle<br>
2. 当Doodle到达窗口的边界（左边或右边）时，它可以从左边边界移动到右边；反則之亦然<br>
3. 玩家可以通過按下**enter键**来发射怪物，并获得分數<br>
4. Doodle有三个生命值，当不小心到接觸Monster、Hazard或Enemy时，其生命值-1<br>
5. 当Doodle获得硬币时，分數+1<br>
6. 游戲設計了两种类型的平台，分別是木頭平台與草地平台<br>
7. 当踩到木头平台时，木头平台会断裂，Doodle會掉下来<br>
8. 当踩在绿色平台上时，Doodle可以稳定地站在上面<br>

**注：当生命值=0时，游戏将结束；反之則游戏繼續**

## **Project Requirements**
- **金幣：** 将分数+1
- **帽子：** 拿到帽子Doodle可以跳得更高
- **子弹：** 在按下"空格键"时向怪物发射子弹
- **分數：** 得到硬币时增加
- **生命：** 初始化为3，当Doodle碰到Monster、Hazard或Blackhole時生命值-1
- **木头平台：** 踩在上面1秒钟，木头平台就会消失，Doodle就會往下掉
- **草地平台：** 可以稳定地站在上面
- **Monster、Hazard、Blackhole、Enemy：** 要避開他們，否則碰到生命值將-1

## **Project Archievement**
Monster2 是 Monster1 的 Polymorphism，Enermy2 是 Enermy1 的 Polymorphism

## **Project Bonus**
- **背景音乐：** 在游戏窗口开始时播放
- **子弹音乐：** 子弹发射时播放
- **背景墙纸：** 游戲背景選用經典Doodle方格子背景 
- **面部朝向：** 当按下特定的方向（向上、向左、向右）時Doodle臉部方向會改变。

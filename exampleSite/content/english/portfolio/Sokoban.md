---
title: "Sokoban"
date: 2021-07-30T12:14:34+06:00
image: "images/portfolio/sokoban.jpg"
categories: ["design","development"]
description: "This is meta description."
draft: false
project_info:
- name: "Completer"
  icon: "fas fa-user"
  content: "Yi-Ting Yang"
- name: "Project Link"
  icon: "fas fa-link"
  content: "https://github.com/yangyang0611/Sokoban-QT"
- name: "Demo Link"
  icon: "fas fa-video"
  content: "
  Level1: <br>https://youtu.be/Hg6UBr1PCPw<p>
  Level2: <br>https://youtu.be/8wsWQrE9X9Y<p>
  Get CANDY finish level: <br>https://youtu.be/cykwuijaaao<p>
  Get BOOM switch level: <br>https://youtu.be/OKo4DM6zHmY"
---

This game is called Sokoban.

## **Project Details**
1. Player can move to 4 directions(up,down,left,right)controlled by keyboard.<br>
2. When start the game,for example in level 1, you as the player is at the entre.<br>
3. Your mission is to push the box into specific place(yellow dots).<br>
4. If the box meet the wall, it cannot move further, same as player.<br>
5. You cannot move the box when they are in line side by side, this will happen a box missing.<br>

**caution(when move left key, wait for 2 sec for the triggle action, or the game will run wrong)**

## **Features**
- **Main menu:** A startButton, restartButton, quitButton, choose levelButton is showned at the top of the window<br>
- **Game items:** If player get boom(purple dot), player can switch level<br>(level 1 ---> level 2 or level 2 ---> level 1), depends on which level he is right now<br>
- **Collection:** If player get coins(big yellow dot), 10 scores will be added<br>
- **Other special method:** If player get candy, he win the game directly
- **Number of step:** Shown at the bottom of map(caution: it will continue count when player is moving except meeting the wall, so need to be careful)<br>

## **Bonus**
**Player state:** When move direction, player will have 4 different states(front face, back face, left face, right face)

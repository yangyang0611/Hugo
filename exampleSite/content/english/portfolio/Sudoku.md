---
title: "Sudoku"
date: 2021-07-30T12:14:34+06:00
image: "images/portfolio/sudoku.jpg"
categories: ["design","development"]
description: "This is meta description."
draft: false
project_info:
- name: "Completer"
  icon: "fas fa-user"
  content: "Yi-Ting Yang"
- name: "Project Link"
  icon: "fas fa-link"
  content: "https://github.com/yangyang0611/Sudoku"
- name: "Demo Link"
  icon: "fas fa-video"
  content: ""
---

This is a game where user input an unsolved sudoku problem, system can generate the solved answer. Furthermore, distinguish if it is have single solve, multiple solve or no answer.The present of sudoku can also be changed with certain commands.

## **Input / Output**
### **Generate**
1. Output sudoku problem when execution

#### **Example**
```shell=
$ ./generate
3 0 2 0 0 5 6 9 0
0 4 0 0 9 6 0 3 0
0 5 0 0 0 8 0 0 0
1 9 0 0 8 0 7 0 3
0 0 0 0 0 0 0 0 0
5 0 7 0 3 0 0 6 1
0 0 0 8 0 0 0 2 0
0 8 0 9 6 0 0 7 0
0 6 5 7 0 0 3 0 9
```

### **Transform**
1. input sudoku problem
2. input transform command
3. output transformed sudoku

#### **Command Format**
- **quit:** 0<br>
- **changeNum:** 1 x y<br>
- **chengeRow** 2 x y<br>
- **changeCol:** 3 x y<br>
- **clockwise rotate 90 degree x times:** 4 x<br>
- **0 is up-down flip, 1 is left-right flip:** 5 x<br>

#### **Example**
```shell=
$ ./transform
## input problem
3 0 2 0 0 5 6 9 0
0 4 0 0 9 6 0 3 0
0 5 0 0 0 8 0 0 0
1 9 0 0 8 0 7 0 3
0 0 0 0 0 0 0 0 0
5 0 7 0 3 0 0 6 1
0 0 0 8 0 0 0 2 0
0 8 0 9 6 0 0 7 0
0 6 5 7 0 0 3 0 9
## command
1 1 9
2 0 1
3 1 2
4 1
5 1
0
## output
9 0 5 3 0 0 0 0 0
1 0 0 0 4 5 0 8 6
0 0 7 2 0 0 0 0 5
7 0 0 6 0 0 0 0 3
0 0 6 1 3 0 2 7 0
3 0 9 0 0 0 0 0 1
0 0 0 0 0 0 8 1 7
8 0 3 0 1 0 0 6 0
0 0 0 5 6 8 0 0 0
```

### **Solve**
1. input sudoku problem
2. output solved sudoku

#### **Output format**
```shell=
## Unsolvable
0
## Solved
1
3 7 2 1 4 5 6 9 8
8 4 1 2 9 6 5 3 7
9 5 6 3 7 8 2 1 4
1 9 4 6 8 2 7 5 3
6 3 8 5 1 7 9 4 2
5 2 7 4 3 9 8 6 1
7 1 9 8 5 3 4 2 6
2 8 3 9 6 4 1 7 5
4 6 5 7 2 1 3 8 9
## Multiple answer
2
```

#### **Example**
```shell=
$ ./solve
## input
3 0 2 0 0 5 6 9 0
0 4 0 0 9 6 0 3 0
0 5 0 0 0 8 0 0 0
1 9 0 0 8 0 7 0 3
0 0 0 0 0 0 0 0 0
5 0 7 0 3 0 0 6 1
0 0 0 8 0 0 0 2 0
0 8 0 9 6 0 0 7 0
0 6 5 7 0 0 3 0 9
## output
1
3 7 2 1 4 5 6 9 8
8 4 1 2 9 6 5 3 7
9 5 6 3 7 8 2 1 4
1 9 4 6 8 2 7 5 3
6 3 8 5 1 7 9 4 2
5 2 7 4 3 9 8 6 1
7 1 9 8 5 3 4 2 6
2 8 3 9 6 4 1 7 5
4 6 5 7 2 1 3 8 9
``
---
title: 红外测速
tags:
  - null
cover: /img/RUN.png
categories:
  - null
date: 2023-10-15 16:20:01
description: Infrared-velocimetry
---
# 需求
我想要在不接触的情况下测量一个小玻璃弹珠的速度，最开始买了几个常用的红外管结果发现触发性能不达标，速度在3m/s以上时就会无法检测到。首先要高速，最好能测量几十米每秒的速度，然后最好便携一点

# 方案
找了一个看起来不错的光电管`IR12-21C/TR8`和`PT12-21B/TR8`，价格也很感人就是了，然后前后两个板子用同一个PCB，板对板连接，然后连接到外置的单片机

# PCB
| ![](微信截图_20231015162424.png)  | ![](微信截图_20231015162438.png)  | ![](微信截图_20231015162455.png)  |
| :------------: | :------------: | :------------: |
| 原理图  | PCB  | 3D模型  |
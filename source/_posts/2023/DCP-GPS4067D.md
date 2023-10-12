---
title: 电磁炉：使用IGBT主动关断控制
tags:
  - 电磁炉
  - 电力电子
cover: /img/fbq.png
categories:
  - null
date: 2023-10-10 12:31:00
description: 使用IGBT：GPS4067D主动关断的进阶版本
---
# 主动关断概述
之前已经完成了一个使用晶闸管的版本，晶闸管的缺点就是无法控制关闭，线圈电流只能等电容完全放电完成和二极管反向短路放电完成之后才能完全归零，这段时间仍然会产生磁场吸引炮弹，导致反拉，反而降低速度，所以需要主动关断停止电容放电，同时线圈也应该在续流二极管上串联电阻加速反向电流衰减。

同时主动关断可以让电容在放电之后仍有一定能量储存，便于下一次升压发射，也就是说减少下一次发射充电时间，连发速度更快

有一篇文章讲了相关内容：[浅谈电炮能量回收——斩波电路与绕组能量回收](https://www.kechuang.org/t/87752)

放一个IGBT的参数在这：IRGPS4067D
![](QQ截图20230626014726.png)
# 实操
## 电路设计1.0
目前的电路设计原理上没什么问题，用直流电源30V测试工作良好。主要是当充电电压大于300V时线圈位置有可能会有电火花，同时IGBT击穿，初步判断是PCB的电容和线圈距离过小直接击穿线圈绝缘层或者线圈本身被击穿

以及光耦提供的驱动电流有限，PC817C只能提供0.2A的驱动电流，IGBT栅极有几十us的上升时间，不知道是不是导致损坏的原因

| ![](QQ截图20231010124847.png)  | ![](QQ截图20231010124819.png)  |
| :------------: | :------------: |
| 原理图  | PCB模型  |

## 电路设计2.0
针对之前的问题，首先使用tc2244驱动芯片来驱动IGBT提高栅极驱动速度，然后电容和线圈分开放置防止隔空击穿

PCB绘制中......
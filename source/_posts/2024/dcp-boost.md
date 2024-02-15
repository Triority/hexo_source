---
title: boost拓扑的电磁炉
tags:
  - 电磁炉
cover: /img/RUN.png
categories:
- 折腾记录
date: 2024-02-02 22:38:32
description: 第一代成品
---
# 关于
之前关于电磁炉的文章都是按照拓扑结构的实验顺序进行的，但是出现了一些问题，首先是折腾这么久晶闸管大力砖飞的方案已经懒得继续做了，然后半桥拓扑不仅效果没有boost拓扑好，甚至还比boost更贵，所以既然之前晶闸管的方案已经做好了也就懒得做半桥了，直接做boost了

前面写的文章也不打算删掉了，毕竟失败的经验也可以供后人参考，而且一些内容可能我已经觉得习以为常但是其他人不太懂。所以这篇文章是经过验证的内容的进展，也就是具体的制作过程，如果有缺失的内容还是去前面的文章找吧。

# 设计目标

+ 出速80m/s以上(目前使用的是6x28)
+ 每秒连发速度大于1
+ 便于拆卸组装

# 电路设计
整体上电路设计为4个PCB，一个为放电电路，一个为控制电路，一个供电电路，一个用于连接电感的PCB板。

其中，放电电路用于承载放电功率元器件，考虑到电路重复性较高为了降低成本，这一部分尽量使用拼版堆叠，M3螺丝连接传输线路，隔离控制线路使用xh2.54连接线。

供电电路用于提供电源，输入为3S电池的12V电压，首先是逆变输出500V给电容充电，然后5V给控制电路的单片机，18V电压用于导通IGBT

控制电路就比较简单，暂时用esp32模组作为主控

## 电源板
电源板用于为放电电路和控制电路提供电源。12V先用ZVS逆变到高频交流再经过变压器升压，经过电容限流，再逆变后得到高压直流输出。


## 下一版改进方向
+ zvs不够稳定计划改为sg3525驱动的推挽升压
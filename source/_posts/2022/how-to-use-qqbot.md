---
title: 丁仪QQ机器人使用说明
excerpt: MPG的成员经常发生变化,此时就需要一个文档来告诉管理们如何使用管理员的道具:群机器人
index_img: /img/aboutqqbot.png
date: 2022-06-16 22:43:01
categories: 
- 其他
tags:
- 文档
- QQ机器人
- python
- linux
---
## 首先,欢迎您成为MPG的一员
丁仪机器人旨在帮助管理员进行群管理,所以请认真按照群规使用,切勿滥用权力,成员记分达到12将被踢出

**注:所有的`<QQ号>`都与`<艾特某群员代替>`完全等价!!随时可以替换!**

**新成员加入时会报告新成员记分数，如果大于等于12请直接踢出**

### 机器人命令语法[MPG专用命令]
#### 1.记分
```
记分 <记分分数> <QQ号> <记分理由>
```
不要忘记空格!!!	不要写反分数和QQ号!!!	不要不写理由!!!
#### 2.清零
```
清零 <QQ号>
```
清零不仅删除现有分数,还会删除全部历史记录!!!
#### 3.记分明细查询
```
明细 <QQ号>
```
可查询此群员全部记录,包括分数,时间,原因,记分操作者
#### 4.查看全部数据
```
穷举
```
##### **这里的穷举将会输出保存的全部数据,直接使用将会造成刷屏,仅限调试程序时使用**

### 机器人命令语法[公共命令]
#### 1.分数查询
```
查分 <QQ号>
```
查询任何人现有总分数.

有任何问题或建议,欢迎随时联系丁仪,包括MPG成员变动导致的使用权限变化
机器人应且只应用于群管,请勿用于其他用途

### 其实还有个隐藏公共命令，欢迎大家探索
{% spoiler QQ号<艾特xxx>--获取被艾特的人的QQ号 %}

### 机器人命令语法[最高级命令]
```
op <QQ号>
```
```
deop <QQ号>
```
将某人添加入或清除出MPG成员列表
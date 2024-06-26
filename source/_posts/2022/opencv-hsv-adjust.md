---
title: opencv-hsv辅助调参工具
date: 2022-10-29 00:10:23
tags:
- opencv
- python
description: opencv经常使用颜色识别某一物体，而找到这一参数范围极其麻烦，因此写了这个程序来帮助确认最佳参数
cover: /img/opencv-hsv-adjust.png
categories: 
- 折腾记录
---
## 前言
opencv经常使用颜色识别某一物体，而找到这一参数范围极其麻烦，因此写了这个程序来帮助确认最佳参数
效果如下：
![识别蓝色锥桶效果](/img/opencv-hsv-adjust.png)
## 代码
> 2023年末的比赛中，学弟为这个程序添加了一些小功能，比如按键保存参数，[博客链接](https://qwqpap.xyz/2023/12/%e6%99%ba%e8%83%bd%e8%bd%a618%e5%b1%8aros%e7%bb%84%e8%a7%86%e8%a7%89%e6%96%b9%e6%a1%88/)

```python
import cv2
import numpy as np
import time

# 'camera' or 'picture'
mode = 'camera'

if mode == 'camera':
    cap = cv2.VideoCapture(0)


def update(x):
    global gs, erode, Hmin, Smin, Vmin, Hmax, Smax, Vmax, img, Hmin2, Hmax2, img0, size_min

    if mode == 'camera':
        ret, img0 = cap.read()
    elif mode == 'picture':
        img0 = cv2.imread('test.jpg')
    img = img0.copy()

    gs = cv2.getTrackbarPos('gs', 'image')
    erode = cv2.getTrackbarPos('erode', 'image')
    Hmin = cv2.getTrackbarPos('Hmin1', 'image')
    Smin = cv2.getTrackbarPos('Smin', 'image')
    Vmin = cv2.getTrackbarPos('Vmin', 'image')
    Hmax = cv2.getTrackbarPos('Hmax1', 'image')
    Smax = cv2.getTrackbarPos('Smax', 'image')
    Vmax = cv2.getTrackbarPos('Vmax', 'image')
    Hmin2 = cv2.getTrackbarPos('Hmin2', 'image')
    Hmax2 = cv2.getTrackbarPos('Hmax2', 'image')
    size_min = cv2.getTrackbarPos('size_min', 'image')
    # 滤波二值化
    gs_frame = cv2.GaussianBlur(img, (gs, gs), 1)
    hsv = cv2.cvtColor(gs_frame, cv2.COLOR_BGR2HSV)
    erode_hsv = cv2.erode(hsv, None, iterations=erode)
    inRange_hsv = cv2.inRange(erode_hsv, np.array([Hmin, Smin, Vmin]), np.array([Hmax, Smax, Vmax]))
    inRange_hsv2 = cv2.inRange(erode_hsv, np.array([Hmin2, Smin, Vmin]), np.array([Hmax2, Smax, Vmax]))
    img = inRange_hsv + inRange_hsv2
    # 外接计算
    cnts = cv2.findContours(img, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)[-2]
    target_list = []
    pos = []
    if size_min < 1:
        size_min = 1
    for c in cnts:
        if cv2.contourArea(c) < size_min:
            continue
        else:
            target_list.append(c)
    for cnt in target_list:
        x, y, w, h = cv2.boundingRect(cnt)
        cv2.rectangle(img0, (x, y), (x + w, y + h), (0, 255, 0), 2)
        pos.append([int(x + w / 2), y + h / 2])
    print(pos)


def img_test():
    sleep = 0.1
    gs = 0
    erode = 0
    Hmin1 = 100
    Hmax1 = 125
    Hmin2 = 179
    Hmax2 = 0
    Smin = 130
    Smax = 255
    Vmin = 50
    Vmax = 240
    size_min = 1000

    # 创建窗口
    cv2.namedWindow('image', cv2.WINDOW_NORMAL)
    cv2.createTrackbar('gs', 'image', 0, 8, update)
    cv2.createTrackbar('erode', 'image', 0, 8, update)
    cv2.createTrackbar('Hmin1', 'image', 0, 179, update)
    cv2.createTrackbar('Hmax1', 'image', 0, 179, update)
    cv2.createTrackbar('Hmin2', 'image', 0, 179, update)
    cv2.createTrackbar('Hmax2', 'image', 0, 179, update)
    cv2.createTrackbar('Smin', 'image', 0, 255, update)
    cv2.createTrackbar('Smax', 'image', 0, 255, update)
    cv2.createTrackbar('Vmin', 'image', 0, 255, update)
    cv2.createTrackbar('Vmax', 'image', 0, 255, update)
    cv2.createTrackbar('size_min', 'image', 1, 100000, update)
    # 默认值
    cv2.setTrackbarPos('gs', 'image', gs)
    cv2.setTrackbarPos('erode', 'image', erode)
    cv2.setTrackbarPos('Hmin1', 'image', Hmin1)
    cv2.setTrackbarPos('Hmax1', 'image', Hmax1)
    cv2.setTrackbarPos('Hmin2', 'image', Hmin2)
    cv2.setTrackbarPos('Hmax2', 'image', Hmax2)
    cv2.setTrackbarPos('Smin', 'image', Smin)
    cv2.setTrackbarPos('Smax', 'image', Smax)
    cv2.setTrackbarPos('Vmin', 'image', Vmin)
    cv2.setTrackbarPos('Vmax', 'image', Vmax)
    cv2.setTrackbarPos('size_min', 'image', size_min)
    while (True):
        try:
            update(1)
        except:
            pass
        cv2.imshow('image', img)
        cv2.imshow('image1', img)
        cv2.imshow('image0', img0)
        time.sleep(sleep)
        if cv2.waitKey(1) == 27:
            break
    cv2.destroyAllWindows()


if __name__ == '__main__':
    img_test()

```
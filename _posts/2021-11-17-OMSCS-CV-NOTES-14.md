---
layout: article
title: OMSCS-CV课程笔记14-Action Recognition
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-14
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍视频分析和动作识别的相关内容。
<!--more-->

## Video Analysis

### Background Subtraction

在视频分析中我们把图像序列看成是一个三维的数组$I(x, y, t)$，通过视频分析我们可以从图像序列中识别出运动的物体。视频分析的一个经典应用是**背景差分(background subtraction)**，我们可以从视频中对背景图像进行建模并通过差分的方式来获得前景图像：

<div align=center>
<img src="https://i.imgur.com/2GM3pf6.png" width="70%">
</div>

背景差分在交通摄像头监控、行为识别、目标跟踪等很多领域都有相关的应用，它的基本流程如下：

1. 估计$t$时刻的背景图像；
2. 将当前图像与背景图像相减，得到差分图像；
3. 对差分图像进行阈值化，得到前景图像的掩码。

显然背景差分最重要的一步是对背景图像进行建模，最简单的方式是使用前一帧的图像作为背景：

$$
B(x, y, t) = I(x, y, t-1)
$$

然而这种方法容易收到运动物体的外观、速度等因素的影响，因此实际中基本不会直接使用之前的图像作为背景。比较常用的背景建模方式是使用均值或者中值图像，通过前$n$帧的图像进行均值滤波或是中值滤波来获得背景：

$$
B(x, y, t) = \frac{1}{n} \sum_{i=1}^n I(x, y, t-i)
$$

$$
B(x, y, t) = \mathop{\text{median}} \{ I(x, y, t-i) \}
$$

背景差分算法的优势在于实现简单、运行效率高、同时对于可变的背景具有一定的适应性；但它的缺陷在于算法的效果容易收到物体运动速度以及视频帧率的影响，而且中值滤波需要存储之前的图像对内存有更高的要求，同时阈值如何设置需要进行不断的调试才能确定。

### Epipolar Plane Images

本节课还介绍了另一种有趣的视频分析应用，称为**极几何图像(epipolar plane images)**。假设物体不动，相机沿直线运动，则空间点$P$会位于同一条极线上：

<div align=center>
<img src="https://i.imgur.com/bU466oT.png" width="50%">
</div>

我们可以把这些图片叠到一起，可以得到图像的长方体：

<div align=center>
<img src="https://i.imgur.com/5O0cmBg.png" width="90%">
</div>

<div align=center>
<img src="https://i.imgur.com/9lXIahO.png" width="30%">
</div>

如果从Y轴进行切片则可以发现空间中同一个点在切片上会变成一条直线，而这条直线的斜率则对应了该点的深度。

<div align=center>
<img src="https://i.imgur.com/Ezggmmc.png" width="30%">
</div>

类似地，我们同样可以对运动的物体构造极几何图像。此时运动的物体会在切片图像上留下特定的图案，一些研究表明我们可以利用这种图案来进行动作的识别。

<div align=center>
<img src="https://i.imgur.com/fm1BG99.png" width="80%">
</div>

## Activity Recognition

## Hidden Markov Models

## Reference
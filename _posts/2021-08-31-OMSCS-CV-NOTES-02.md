---
layout: article
title: OMSCS-CV课程笔记02-Hough Transform
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-02
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍霍夫变换的相关内容。
<!--more-->

## Hough Line Transform

**霍夫变换(Hough transform)**是一种经典的图像处理技术，我们可以通过它来检测图像中的各种几何元素。二维图像中最简单的几何元素是直线，对应的检测算法称为**霍夫线变换(Hough line transform)**。

直线检测的难点在于图像上存在无穷多条直线，使用暴力穷举直线的方法是不可行的。因此霍夫线变换使用了**计数(voting)**的方式来统计图像中可能出现的直线，其思想是只考虑图像中可能出现的直线并进行计数，如果计数结果大于一定的阈值则说明图像上存在该直线。

接下来介绍霍夫线变换的算法原理。我们可以用直线方程来表示平面上通过点$(x, y)$的任意直线：

$$
y = m_0 x + b_0
$$

其中$m_0$和$b_0$是直线的参数。如果把直线方程看做是参数的函数，那么就可以在参数平面来表示直线，即图像平面的一条直线对应参数平面上的一个点。

<div align=center>
<img src="https://i.imgur.com/Ztofz6W.png" width="70%">
</div>

因此图像平面和参数平面存在对偶关系，图像平面上的点也可以用参数平面上的直线来表示：

$$
y = m_0 x + b_0 \Leftrightarrow b_0 = -x m_0 + y
$$

<div align=center>
<img src="https://i.imgur.com/Ezgr9ES.png" width="70%">
</div>

对于图像平面上的两个点$(x_0, y_0)$和$(x_1, y_1)$，我们可以分别在参数平面上画出对应的两条直线，它们的交点即代表图像平面上通过$(x_0, y_0)$和$(x_1, y_1)$的直线。

<div align=center>
<img src="https://i.imgur.com/wPdqN4a.png" width="70%">
</div>

因此我们可以利用参数平面来寻找图像上的直线元素。对于图像上的一系列点我们可以在参数平面上画出它们对应的直线，这些直线的交点即为图像平面上通过这一系列点的直线，交点的坐标为直线方程的参数。

<div align=center>
<img src="https://i.imgur.com/rMW5rYq.png" width="70%">
</div>

在此基础上可以得到霍夫线变换的基本流程如下：

1. 对图像进行边缘检测得到边缘点；
2. 将参数平面划分成网格，每个网格对应图像平面的一条直线，同时初始化网格计数为0；
3. 对边缘点进行遍历，在每个点上考虑参数平面通过该点的所有格子并令格子的计数加1；
4. 完成遍历后统计参数平面网格上的计数，大于阈值的格子即为图像平面上直线方程的参数。

在实际中通常使用极坐标下的直线方程：

$$
x \cos \theta + y \sin \theta = d
$$

在参数平面上考虑$\theta$的所有可能取值并利用$(x, y)$反算出剩下的参数$d$，从而更新参数平面的计数。

<div align=center>
<img src="https://i.imgur.com/buEoPYd.png" width="30%">
</div>

因此霍夫线变换将直线检测的问题转化为参数平面的计数问题，所需的空间复杂度为参数平面网格的大小$O(k^2)$，时间复杂度为边缘点的数量$O(n)$。

在标准流程外我们还可以利用图像梯度的方向显式指定参数$\theta$，或是赋予不同参数不同的权重来提升算法的效果。

## Hough Circle Transform

## Generalized Hough Transform
---
layout: article
title: OMSCS-CV课程笔记01-Linear Image Processing
tags: ["OMSCS", "CV"]
key: OMSCS-CV-01
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍图像处理的基础知识。
<!--more-->

## Image as Functions

图像处理是对图像进行操作，此时我们会把图像看做是一个二元函数$f(x,y)$。对于灰度图像可以认为图像的每一点是一个标量，因此$f$可以表示为：

$$
f:[a, b] \times [c, d] \rightarrow [\min, \max]
$$

其中$[a, b]$和$[c, d]$表示图像的大小范围，$[\min, \max]$表示灰度的范围。对于彩色图像则可以认为$f$的值域是一个向量：

$$
f(x, y) = 
\begin{bmatrix}
r(x, y) \\ g(x, y) \\ b(x, y)
\end{bmatrix}
$$

其中$r(x, y)$，$g(x, y)$，$b(x, y)$分别表示三个通道上的色彩值。

由于计算机不能表示连续的对象，因此计算机中的数字图像实际上是经过离散后的结果，此时我们也可以把图像理解为一个数组或是矩阵。

<div align=center>
<img src="https://i.imgur.com/Pxskgo5.png" width="32%">
<img src="https://i.imgur.com/Pa10JG2.png" width="40%">
</div>

将图像视为函数之后就可以用函数的方法对图像进行操作，其中最简单的操作是对函数进行加减。比如说我们可以把对图像添加噪声的操作理解为原函数$f(x, y)$与噪声函数noise相加。常见的噪声函数包括：

- 椒盐噪声(salt-and-pepper noise)：随机出现的黑白噪点；
- 脉冲噪声(impulse noise)：随机出现的白噪点；
- 高斯噪声(Gaussian noise)：服从正态分布$N(0, \sigma^2)$的噪点。

<div align=center>
<img src="https://i.imgur.com/xGQc9uM.png" width="60%">
</div>

对于高斯噪声，方差$\sigma^2$控制了噪声的强度：方差越大噪声越明显。

## Filtering

## Linearity and Convolution

## Filters as Templates

## Edge Detection: Gradients

## Edge detection: 2D Operators
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

去除图像噪声的过程称为**滤波(filtering)**。尽管精确地还原出无噪声图像是非常困难的，但滤波可以使图像变得更加平滑，也可以实现图像模糊的视觉效果。为了便于讨论我们对噪声做出以下两条假定：

- 每一个像素点不带噪声的真值与它周围的像素值相近；
- 每一个像素点添加的噪声相互独立。

在这样的假设下我们可以使用滑动平均的方法对图像进行滤波，具体地针对每个像素点取它周围像素的平均值作为滤波的结果。假设我们已知图像$F(x,y)$，对它使用滑动平均进行滤波的过程如下：

<div align=center>
<img src="https://i.imgur.com/iCybD4n.png" width="50%">
</div>

<div align=center>
<img src="https://i.imgur.com/VGJ9mqJ.png" width="50%">
</div>

<div align=center>
<img src="https://i.imgur.com/SBpay1T.png" width="50%">
</div>

<div align=center>
<img src="https://i.imgur.com/YaSgCw1.png" width="50%">
</div>

以上过程写成数学表达式为：

$$
G(i, j) = \frac{1}{(2k+1)^2} \sum_{u=-k}^k \sum_{v=-k}^k F(i+u, j+v)
$$

其中$k$为邻域的半径。上述公式表明像素点的邻域对中心的贡献是相同的，每个相邻像素点都具有相同权重。实际中更常用的方法是对邻域中的像素赋予不同的权重，此时公式可以改写为：

$$
G(i, j) = \sum_{u=-k}^k \sum_{v=-k}^k H(u, v) F(i+u, j+v)
$$

其中$H(u, v)$满足$\sum H(u, v) = 1$，它代表邻域内不同像素具有的权重，称为滤波器的**核(kernel)**或者**模板(mask)**。上述的滤波过程称为**相关滤波(correlation filtering)**，记为$G = H \otimes F$。

使用**方块核(box filter)**进行滤波可以图像模糊的效果如下：

<div align=center>
<img src="https://i.imgur.com/ubX9JEI.png" width="30%">
<img src="https://i.imgur.com/GQa2SBz.png" width="30%">
</div>

仔细观察可以发现图像中有很多的方块状伪影。产生这种现象的原因是方块核并不能正确地反映图像模糊的过程：我们可以想象眼前有一个亮点不断离我们远去，随着距离的增加图像应该是中间亮边缘暗的，如下图所示：

<div align=center>
<img src="https://i.imgur.com/23SLRc2.png" width="20%">
</div>

因此要正确的实现图像模糊的效果我们需要类似于上图的核。实际中比较常用的是**高斯核(Gaussian kernel)**，它可以看做是高斯函数的离散形式：

<div align=center>
<img src="https://i.imgur.com/2WtpHvU.png" width="70%">
</div>

使用高斯核代替方块核可以得到更加合理的模糊效果：

<div align=center>
<img src="https://i.imgur.com/ubX9JEI.png" width="30%">
<img src="https://i.imgur.com/zVfSVk4.png" width="30%">
</div>

## Linearity and Convolution

## Filters as Templates

## Edge Detection: Gradients

## Edge detection: 2D Operators
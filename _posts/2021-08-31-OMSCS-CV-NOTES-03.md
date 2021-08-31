---
layout: article
title: OMSCS-CV课程笔记03-Frequency Domain Analysis
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-03
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍频域分析的相关内容。
<!--more-->

## Fourier Transform

在图像处理中我们往往把数字图像视为关于空间位置的函数，实际上从频域角度上来看我们还可以把数字图像看做是一系列给定频率函数的组合，不同频率的函数表示图像在相应方向上的变化快慢。从频域角度认识和分析图像的方法称为频域分析。

以一维信号为例，通过**傅里叶变换(Fourier transform)**我们可以把函数$f(x)$在频域进行表示，得到频域函数$F(u)$：

$$
F(u) = \int_{-\infty}^\infty f(x) e^{-i 2 \pi u x} dx
$$

$F(u)$表示$f(x)$在对应频率$u$上的权重，它的实部和虚部分别表示频率为$u$的余弦和正弦信号成分。

<div align=center>
<img src="https://i.imgur.com/Fif1pte.png" width="90%">
</div>

与之对应的，通过**逆傅里叶变换(inverse Fourier transform)**可以将频域函数$F(u)$变换为时域函数$f(x)$：

$$
f(x) = \int_{-\infty}^\infty F(u) e^{i 2 \pi u x} du
$$

需要说明的是傅里叶变换仅在函数可积时成立，即函数$f(x)$需要满足：

$$
\int_{-\infty}^\infty \vert f(x) \vert dx < \infty
$$

将傅里叶变换推广到在离散情况，可以得到信号处理中常用的**离散傅里叶变换(discrete Fourier transform, DFT)**：

$$
F(k) = \frac{1}{N} \sum_{x=0}^{N-1} f(x) e^{-i \frac{2 \pi k x}{N}}
$$

对于数字图像我们需要将傅里叶变换应用到二维平面上，得到连续和离散形式的二维傅里叶变换：

$$
F(u, v) = \int_{-\infty}^\infty \int_{-\infty}^\infty f(x, y) e^{-i 2 \pi (ux + vy)} dx dy
$$

$$
F(k_x, k_y) = \frac{1}{N} \sum_{x=0}^{N-1} \sum_{y=0}^{N-1} f(x, y) e^{-i \frac{2 \pi (k_x x + k_y y)}{N}}
$$

在数字图像的频域分析中通常只关注频域图像$F(k_x, k_y)$的幅度而忽略相位，将$F(k_x, k_y)$的幅度进行可视化就得到了数字图像的**频谱(frequency spectrum)**。图像的频谱在某个位置的响应越强表示图像在该方向变化越剧烈：

<div align=center>
<img src="https://i.imgur.com/Z5Wg0Rh.png" width="25%">
<img src="https://i.imgur.com/HbGBH7u.png" width="25%">
</div>

<div align=center>
<img src="https://i.imgur.com/2YogQt5.png" width="25%">
<img src="https://i.imgur.com/BHKDIb2.png" width="25%">
</div>

同时由于傅里叶变换具有可加性，两幅图像相加后它们的频谱也会相加：

<div align=center>
<img src="https://i.imgur.com/AeQ2ND1.png" width="70%">
</div>

此外对频谱进行操作也会反映到图像上。删去频谱的高频成分相当于对图像进行模糊，而删去低频成分则相当于提取图像的边缘。

<div align=center>
<img src="https://i.imgur.com/811Fa2o.png" width="40%">
<img src="https://i.imgur.com/FLtAPqa.png" width="40%">
</div>

## Convolution in Frequency Domain

卷积运算与频域分析有着深刻的联系。以一维信号为例，假设信号$g$为$f$和$h$的卷积$g = f * h$，此时$g$的频域形式为：

$$
\begin{aligned}
G(u) &= \int_{-\infty}^\infty g(x) e^{-i 2 \pi u x} dx \\
&= \int_{-\infty}^\infty \int_{-\infty}^\infty f(\tau) h(x - \tau) e^{-i 2 \pi u x} d \tau dx \\
&=\int_{-\infty}^\infty \int_{-\infty}^\infty [f(\tau) e^{-i 2 \pi u \tau}] [h(x - \tau) e^{-i 2 \pi u (x - \tau)}] d \tau dx \\
&= \int_{-\infty}^\infty f(\tau) e^{-i 2 \pi u \tau} d \tau \int_{-\infty}^\infty h(x') e^{-i 2 \pi u x'} dx' \\
&=F(u) H(u)
\end{aligned}
$$

上式说明在时域函数的卷积相当于频域函数的乘积，称为**卷积定理(convolution theorem)**。类似地可以证明频域函数的卷积等价于时域函数的乘积。

通过卷积定理我们还可以从频域的角度来认识卷积滤波。以高斯滤波为例，从频域上看使用高斯核进行滤波相当于保留了图像的低频成分同时抑制了高频成分。由于滤波去掉了高频信息(细节)，图像自然会变得模糊。

<div align=center>
<img src="https://i.imgur.com/4SbCZaU.png" width="70%">
</div>

除了卷积定理外，傅里叶变换的其他常用性质包括：

- Linearity：$c_1 f(x) + c_2 g(x) \Leftrightarrow c_1 F(x) + c_2 G(x)$
- Scaling：$f(ax) \Leftrightarrow \frac{1}{\vert a \vert} F(\frac{u}{a})$
- Differentiation：$\frac{d^n}{d x^n} f(x) \Leftrightarrow (i 2 \pi u)^n F(u)$

同时一些常用函数的傅里叶变换如下：

<div align=center>
<img src="https://i.imgur.com/JnEx6sX.png" width="70%">
</div>

## 	Aliasing
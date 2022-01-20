---
layout: article
title: OMSCS-SIM课程笔记02-Calculus, Probability, and Statistics Primers
tags: ["OMSCS", "ISYE6644-SIM"]
key: OMSCS-SIM-02
aside:
  toc: true
sidebar:
  nav: OMSCS-SIM
---

> 这个系列是Gatech OMSCS 仿真和建模课程([ISYE 6644: Simulation and Modeling for Engineering and Science](https://omscs.gatech.edu/isye-6644-simulation-and-modeling-engineering-and-science))的同步课程笔记。课程内容涉及计算机模拟在统计分析和建模中的应用，本节主要复习微积分以及概率论的相关知识。
<!--more-->

## Calculus Primer

在进一步介绍随机模拟的内容前首先来回顾一下微积分中的基本内容。

<div align=center>
<img src="https://i.imgur.com/EOUMhdr.jpg" width="80%">
<img src="https://i.imgur.com/8IpC0tR.jpg" width="80%">
<img src="https://i.imgur.com/Q44MQnh.jpg" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/5fWyWHB.jpg" width="78%">
<img src="https://i.imgur.com/LQ3i4He.jpg" width="78%">
<img src="https://i.imgur.com/qW8WkjV.jpg" width="78%">
</div>

一些常用函数的导数如下：

$$
[x^k]' = k x^{k-1}
$$

$$
[e^x]' = e^x
$$

$$
[\sin (x)]' = \cos (x)
$$

$$
[\cos (x)]' = -\sin (x)
$$

$$
[\ln (x)]' = \frac{1}{x}
$$

$$
[\arctan (x)]' = \frac{1}{1 + x^2}
$$

同时，导数的运算法则为：

$$
[a f(x) + b]' = a f'(x)
$$

$$
[f(x) + g(x)]' = f'(x) + g'(x)
$$

$$
[f(x) g(x)]' = f'(x) g(x) + f(x) g'(x)
$$

$$
\bigg[ \frac{f(x)}{g(x)} \bigg]' = \frac{g(x) f'(x) - f(x) g'(x)}{g^2 (x)}
$$

$$
[f(g(x))]' = f'(g(x)) g'(x)
$$

函数$f(x)$仅在其导数为0的位置取极值，而借助于二阶导数我们还可以进一步判断极值点的类型。

<div align=center>
<img src="https://i.imgur.com/O4C9DTm.jpg" width="80%">
<img src="https://i.imgur.com/l99hEFq.jpg" width="80%">
<img src="https://i.imgur.com/yRTCQs6.jpg" width="80%">
<img src="https://i.imgur.com/gapqWiE.jpg" width="80%">
</div>

## Finding Zeros

在很多时候我们需要去计算函数的零点。对于复杂的函数可能无法解析地求得函数的零点，在这种情况下需要使用一些数值计算方法来求解。最基本的方法是**二分法(bisection)**：

<div align=center>
<img src="https://i.imgur.com/FK7YfdR.jpg" width="80%">
</div>

除了二分法之外我们还可以通过**Newton's method**来迭代计算函数的零点。

<div align=center>
<img src="https://i.imgur.com/kWZpm2U.jpg" width="80%">
</div>

$$
x_{i+1} = x_i - \frac{g(x_i)}{g'(x_i)}
$$

## Integration

除了微分之外，我们还需要计算积分。

<div align=center>
<img src="https://i.imgur.com/koVKCub.jpg" width="80%">
<img src="https://i.imgur.com/VZNQw5I.jpg" width="80%">
</div>

常用函数的积分公式如下：

$$
\int x^k dx = \frac{x^{k+1}}{k+1} + C, k \neq -1
$$

$$
\int \frac{dx}{x} dx = \ln \vert x \vert + C
$$

$$
\int e^x dx = e^x + C
$$

$$
\int \cos (x) dx = \sin (x) + C
$$

$$
\int \frac{dx}{1 + x^2} = \arctan (x) + C
$$

(定)积分的常用性质为：

$$
\int_a^a f(x) dx = 0
$$

$$
\int_a^b f(x) dx = - \int_b^a f(x) dx
$$

$$
\int_a^b f(x) dx = \int_a^c f(x) dx + \int_c^b f(x) dx
$$

$$
\int [f(x) + g(x)] dx = \int f(x) dx + \int g(x) dx
$$

$$
\int f(x) g'(x) dx = f(x) g(x) - \int g(x) f'(x) dx
$$

$$
\int f(g(x)) g'(x) dx = \int f(u) du
$$

### Riemann Sums

对于复杂的函数，有时可能很难通过解析的形式来计算定积分。此时我们可以将函数拆分成若干个小区间然后在每个区间上计算函数包围的面积，最后把它们加起来近似定积分的值。这种做法称为黎曼和(Riemann sums)：

<div align=center>
<img src="https://i.imgur.com/U3BPt2S.jpg" width="80%">
</div>

### Taylor Series Expansion

在微积分中**泰勒级数展开(Taylor series expansion)**是一种非常常用的方法：

<div align=center>
<img src="https://i.imgur.com/x6MpwFu.jpg" width="80%">
</div>

在$a=0$处进行展开得到的级数称为Maclaurin级数，常用函数的Maclaurin级数为：

$$
\sin (x) = \sum_{k=0}^\infty \frac{(-1)^k x^{2k + 1}}{(2k + 1)!}
$$

$$
\cos (x) = \sum_{k=0}^\infty \frac{(-1)^k x^{2k}}{(2k)!}
$$

$$
e^x = \sum_{k=0}^\infty \frac{x^k}{k!}
$$

另一个常用的工具是**洛必达法则(L'Hospital's rule)**，它指出当极限存在时可以利用函数的导数来代替函数值计算极限：

<div align=center>
<img src="https://i.imgur.com/bCweIqe.jpg" width="70%">
</div>

## Probability Basics

### Probabilities

接下来复习一下概率论的相关知识。

<div align=center>
<img src="https://i.imgur.com/WdPvNR2.jpg" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/7i2shoo.jpg" width="80%">
</div>

### Random Variables

<div align=center>
<img src="https://i.imgur.com/RzUg9Ja.jpg" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/JiXLH3c.jpg" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/DoxdVLe.jpg" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/twpvTdQ.jpg" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/vt84Thk.jpg" width="80%">
</div>

## Simulating Random Variables

那么如何使用计算机来产生各种类型的随机变量呢？对于任意连续型随机变量$X$我们可以通过它的CDF来进行采样，实际上$F(X)$服从(0, 1)区间上的均匀分布：

<div align=center>
<img src="https://i.imgur.com/ONHtqto.jpg" width="70%">
</div>

稍后我们会来证明这个定理。由于$F(X) \sim \text{Unif} (0, 1)$，我们可以通过对(0, 1)区间上的均匀分布进行采样再映射回$X$实现对任意分布的采样，这种采样方法称为**逆变换方法(inverse transform method)**。以参数为$\lambda$的指数分布为例，假设$X \sim \text{Exp} (\lambda)$则它的CDF为$F(X) = 1 - e^{-\lambda X}$，根据逆变换方法可以得到采样公式为：

$$
X = - \frac{1}{\lambda} \ln (1 - U), \ U \sim \text{Unif} (0, 1)
$$

对于逆变换方法我们需要生成(0, 1)区间上的均匀分布的随机数，我们可以利用上节课介绍的[伪随机数生成算法](/2022/01/16/OMSCS-SIM-NOTES-01.html#generating-randomness)来实现：

<div align=center>
<img src="https://i.imgur.com/99sOakO.jpg" width="80%">
</div>

## Great Expectations

期望是随机变量的一个重要性质，离散和连续型随机变量的期望分别定义为：

<div align=center>
<img src="https://i.imgur.com/mlQQeF1.jpg" width="80%">
</div>

常用分布的期望如下：

<div align=center>
<img src="https://i.imgur.com/Ld2D6SJ.jpg" width="60%">
</div>

<div align=center>
<img src="https://i.imgur.com/jmRFcSj.jpg" width="60%">
</div>

<div align=center>
<img src="https://i.imgur.com/0xhI99V.jpg" width="68%">
</div>

### LOTUS

对于作用在随机变量上的函数，我们可以利用**law of the unconscious statistician(LOTUS)**来计算它的期望：

<div align=center>
<img src="https://i.imgur.com/Q1BfpMI.jpg" width="80%">
</div>

函数$h(X)$可以是任意形式，而对于幂函数我们称对应的期望为$X$的**n阶矩($n$th moment of $X$)**。除了幂函数我们还可以利用LOTUS来定义**n阶中心矩($n$th central moment of $X$)**和**方差(variance)**：

<div align=center>
<img src="https://i.imgur.com/cqiZ8pe.jpg" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/e3SZJE8.jpg" width="70%">
</div>

<div align=center>
<img src="https://i.imgur.com/laWzyB9.jpg" width="70%">
</div>

期望和方差的一个重要性质是线性性：

<div align=center>
<img src="https://i.imgur.com/2GXb4pA.jpg" width="80%">
</div>

### Moment Generating Functions

和期望有关的另一个函数是**动量母函数(moment generating functions, MGF)**：

<div align=center>
<img src="https://i.imgur.com/Cg2Cs2J.jpg" width="70%">
</div>

常用分布的MGF为：

<div align=center>
<img src="https://i.imgur.com/uZ9CZCv.jpg" width="70%">
</div>

<div align=center>
<img src="https://i.imgur.com/cMgct85.jpg" width="70%">
</div>

我们可以通过对MGF求导来计算$X$的n阶矩：

<div align=center>
<img src="https://i.imgur.com/5rwFJMQ.jpg" width="70%">
</div>
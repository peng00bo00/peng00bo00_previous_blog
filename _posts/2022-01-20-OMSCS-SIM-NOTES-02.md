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
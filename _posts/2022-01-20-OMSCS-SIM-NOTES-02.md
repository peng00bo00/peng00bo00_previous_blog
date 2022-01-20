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

函数$f(x)$仅在其导数为0的位置取极值，而借助于二阶导数，我们还可以判断函数的极值点类型。

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
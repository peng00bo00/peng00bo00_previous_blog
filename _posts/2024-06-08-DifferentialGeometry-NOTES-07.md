---
layout: article
title: 微分几何笔记07-活动标架和外微分法
tags: ["CG", "Geometry Processing", "Math", "Differential Geometry"]
key: DifferentialGeometry-07
aside:
  toc: true
sidebar:
  nav: DifferentialGeometry
---

> 这个系列是北京大学陈维桓教授《微分几何(第二版)》的学习笔记，主要涉及古典微分几何中曲线曲面理论的相关知识。系统学习微分几何对于理解计算机图形学中的各种几何处理算法是十分有益的。本节介绍活动标架和外微分法的相关理论。
<!--more-->

## 外形式

本节要在代数上做一些准备，介绍外形式和外代数的概念。

设$$V$$是$$n$$维向量空间，$$\{ \boldsymbol{e}_1, ..., \boldsymbol{e}_n \}$$是它的一个基底，则空间$$V$$中的任意一个元素$$\boldsymbol{x}$$都能够唯一地表示为基底向量$$\boldsymbol{e}_1, ..., \boldsymbol{e}_n$$的线性组合，设为

$$
\boldsymbol{x} = x^1 \boldsymbol{e}_1 + \cdots + x^n \boldsymbol{e}_n \equiv x^i \boldsymbol{e}_i
$$

在最右端我们采用了[Einstein的和式约定](/2023/12/27/DifferentialGeometry-NOTES-05.html#einstein求和约定)。在本节，我们规定所有的指标$$i$$，$$j$$，$$k$$，$$l$$的取值范围是从1到$$n$$的整数。实数$$x^1, ...，x^n$$称为向量$$\boldsymbol{x}$$在基底$$\{ \boldsymbol{e}_1, ..., \boldsymbol{e}_n \}$$下的分量。

设$$f: V \rightarrow \mathbb{R}$$是向量空间$$V$$上的函数。如果对于任意的$$\boldsymbol{x}, \boldsymbol{y} \in V$$及$$\alpha \in \mathbb{R}$$总有

$$
f(\boldsymbol{x} + \boldsymbol{y}) = f(\boldsymbol{x}) + f(\boldsymbol{y}), \ \ \ f(\boldsymbol{x}) = \alpha \cdot f(\boldsymbol{x})
$$

则称$$f$$是向量空间$$V$$上的线性函数。在固定的基底$$\{ \boldsymbol{e}_i \}$$下，取向量$$\boldsymbol{x}\in V$$在该基底下的第$$j$$的分量，显然它是在向量空间$$V$$的一个线性函数，记为$$e^j$$，即

$$
e^j (\boldsymbol{x}) = x^j
$$

特别地，函数$$e^j$$在基底向量$$\boldsymbol{e}_i$$上的值是

$$
e^j (\boldsymbol{e}_i) = 
\begin{cases}
1, & i = j \\
0, & i \neq j
\end{cases}
$$

为方便起见，常常把上式右端记为$$\delta_i^j$$，称作Kronecker $$\delta$$记号，即

$$
\delta_i^j = 
\begin{cases}
1, & i = j \\
0, & i \neq j
\end{cases}
$$

这里的$$\delta_i^j$$是专用记号，与基底$$\{ \boldsymbol{e}_i \}$$所用的字母的记号没有关系。
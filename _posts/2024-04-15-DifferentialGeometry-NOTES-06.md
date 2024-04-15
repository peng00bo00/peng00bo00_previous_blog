---
layout: article
title: 微分几何笔记06-测地曲率和测地线
tags: ["CG", "Geometry Processing", "Math", "Differential Geometry"]
key: DifferentialGeometry-06
aside:
  toc: true
sidebar:
  nav: DifferentialGeometry
---

> 这个系列是北京大学陈维桓教授《微分几何(第二版)》的学习笔记，主要涉及古典微分几何中曲线曲面理论的相关知识。系统学习微分几何对于理解计算机图形学中的各种几何处理算法是十分有益的。本节介绍内蕴几何学中测地曲率和测地线的相关内容。
<!--more-->

由Gauss开创的曲面内蕴几何学有丰富的内容。本章的重点是研究曲面上曲线的测地曲率和测地线，在研究它们的外在特征和性质的同时，更主要的是证明它们可以通过曲面的第一基本形式进行计算，而与曲面的第二基本形式无关。因此它们在曲面的保长对应下是保持不变的，是曲面的内蕴性质。通过本章的学习，使我们了解曲面内蕴几何学的主要研究对象是什么，从而为今后学习黎曼几何学打下基础。

## 测地曲率和测地挠率

### 曲面上曲线的正交标架场

设正则参数曲面$$S$$的方程是$$\boldsymbol{r} = \boldsymbol{r}(u^1, u^2)$$，$$C$$是曲面$$S$$上的一条曲线，它的方程是$$u^\alpha = u^\alpha (s)$$，$$\alpha = 1, 2$$，其中$$s$$是曲线$$C$$的弧长参数。那么$$C$$作为空间$$\mathbb{E}^3$$中曲线的参数方程是

$$
\boldsymbol{r} = \boldsymbol{r} (s) = \boldsymbol{r} (u^1 (s), u^2 (s))
$$

在[曲线论](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的曲率和frenet标架)中我们曾经沿空间曲线$$C$$建立了Frenet标架$$\{ \boldsymbol{r} (s); \boldsymbol{\alpha} (s), \boldsymbol{\beta} (s), \boldsymbol{\gamma}(s) \}$$。但是，曲线$$C$$的Frenet标架场没有考虑到目前的曲线$$C$$落在曲面$$S$$上的事实，因此Frenet标架及其运动公式(Frenet公式)自然不会反映曲线$$C$$和曲面$$S$$之间相互约束的关系。现在，我们要沿曲线$$C$$建立一个新的正交标架场$$\{ \boldsymbol{r}; \boldsymbol{e}_1, \boldsymbol{e}_2, \boldsymbol{e}_3 \}$$，使得它兼顾曲线$$C$$和曲面$$S$$，其定义是

$$
\begin{aligned}
\boldsymbol{e}_1 &= \frac{\mathrm{d} \boldsymbol{r} (s)}{\mathrm{d} s} = \boldsymbol{\alpha} (s) \\
\boldsymbol{e}_3 &= \boldsymbol{n} (s) \\
\boldsymbol{e}_2 &= \boldsymbol{e}_3 \times \boldsymbol{e}_1 = \boldsymbol{n} (s) \times \boldsymbol{\alpha} (s) \\
\end{aligned}
$$

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/DjV5ATz.png" width="80%">
</div>

直观上，向量$$\boldsymbol{e}_2$$是将曲线$$C$$的切向量$$\boldsymbol{e}_1 = \boldsymbol{\alpha}$$围绕曲面$$S$$的单位法向量$$\boldsymbol{n}$$按正向旋转90°得到的。与[Frenet公式](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的挠率和frenet公式)相对照不难发现，我们在这里对于曲面$$S$$上的曲线$$C$$建立正交标架场的做法和平面曲线建立正交标架场的做法是一致的。换言之我们现在的目标是把平面上的曲线论推广成为曲面$$S$$上的曲线论。

首先我们要建立曲面$$S$$上沿曲线$$C$$的正交标架场$$\{ \boldsymbol{r}; \boldsymbol{e}_1, \boldsymbol{e}_2, \boldsymbol{e}_3 \}$$的运动公式。因为这是单位正交标架场，所以可以假设

$$
\begin{cases}
\begin{aligned}
\frac{\mathrm{d} \boldsymbol{r} (s)}{\mathrm{d} s} &= \boldsymbol{e}_1 \\
\frac{\mathrm{d} \boldsymbol{e}_1 (s)}{\mathrm{d} s} &= \kappa_g \boldsymbol{e}_2 + \kappa_n \boldsymbol{e}_3 \\
\frac{\mathrm{d} \boldsymbol{e}_2 (s)}{\mathrm{d} s} &= -\kappa_g \boldsymbol{e}_1 + \tau_g \boldsymbol{e}_3\\
\frac{\mathrm{d} \boldsymbol{e}_3 (s)}{\mathrm{d} s} &= -\kappa_n \boldsymbol{e}_1 - \tau_g \boldsymbol{e}_2\\
\end{aligned}
\end{cases}
$$

其中$$\kappa_g$$，$$\kappa_n$$，$$\tau_g$$是待定的系数函数。很明显，

$$
\kappa_n = \frac{\mathrm{d} \boldsymbol{e}_1 (s)}{\mathrm{d} s} \cdot \boldsymbol{e}_3 (s) = \boldsymbol{r}'' (s) \cdot \boldsymbol{n}
$$

所以$$\kappa_n$$恰好是曲面$$S$$沿曲线$$C$$的切方向的[法曲率](/2023/11/10/DifferentialGeometry-NOTES-04.html#法曲率)。代入上式得到

$$
\kappa_g = \frac{\mathrm{d}^2 \boldsymbol{r} (s)}{\mathrm{d} s^2} \cdot \boldsymbol{e}_2 = \boldsymbol{r}'' (s) \cdot (\boldsymbol{n} (s) \times \boldsymbol{r}' (s)) = \big( \boldsymbol{n} (s), \boldsymbol{r}' (s), \boldsymbol{r}'' (s) \big)
$$

称$$\kappa_g$$为曲面$$S$$上的曲线$$C$$的**测地曲率**。另外

$$
\begin{aligned}
\tau_g &= \frac{\mathrm{d} \boldsymbol{e}_2}{\mathrm{d} s} \cdot \boldsymbol{n} = \frac{\mathrm{d} (\boldsymbol{n} \times \boldsymbol{r}' (s))}{\mathrm{d} s} \cdot \boldsymbol{n} \\
&= (\boldsymbol{n}' (s) \times \boldsymbol{r}' (s)) \cdot \boldsymbol{n} = \big( \boldsymbol{n}, \boldsymbol{n}' (s), \boldsymbol{r}' (s) \big)
\end{aligned}
$$

称$$\tau_g$$为曲面$$S$$上的曲线$$C$$的**测地挠率**。

### 测地曲率

下面我们来讨论曲面$$S$$上的曲线$$C$$的测地曲率的表达式和性质。从$$\kappa_g$$的定义式得到

$$
\begin{aligned}
\kappa_g &= \big( \boldsymbol{n} (s), \boldsymbol{r}' (s), \boldsymbol{r}'' (s) \big) \\
&= \boldsymbol{n} \cdot (\boldsymbol{r}'(s) \times \boldsymbol{r}'' (s)) = \boldsymbol{n} \cdot (\boldsymbol{\alpha} (s) \times \kappa \boldsymbol{ \beta} (s)) \\
&= \kappa \boldsymbol{n} \cdot \boldsymbol{\gamma} (s) = \kappa \cos{\tilde{\theta}}
\end{aligned}
$$

其中$$\tilde{\theta}$$是曲线$$C$$的次法向量$$\boldsymbol{\gamma}$$和曲面$$S$$的法向量$$\boldsymbol{n}$$的夹角，也是曲线$$C$$的主法向量$$\boldsymbol{\beta}$$和曲面$$S$$的切平面的夹角。利用上式$$\boldsymbol{e}_1$$的运动方程还能够写成

$$
\kappa \boldsymbol{\beta} (s) = \kappa_g \boldsymbol{e}_2 + \kappa_n \boldsymbol{n}
$$

所以

$$
\kappa^2 = \kappa_g^2 + \kappa_n^2
$$

根据[法曲率](/2023/11/10/DifferentialGeometry-NOTES-04.html#法曲率)的定义，我们已经知道

$$
\kappa_n = \kappa \cos{\theta}
$$

其中$$\theta$$是曲线$$C$$的主法向量$$\boldsymbol{\beta}$$和曲面$$S$$的法向量$$\boldsymbol{n}$$的夹角。利用法曲率的几何解释可以容易地得到测地曲率的几何解释。

**定理6.1** 设$$C$$是在曲面$$S$$上的一条正则曲线，则曲线$$C$$在点$$p$$的测地曲率等于把曲线$$C$$投影到曲面$$S$$在点$$p$$的切平面上所得的曲线$$\tilde{C}$$在该点的相对曲率，其中切平面的正向由曲面$$S$$在点$$p$$的法向量$$\boldsymbol{n}$$给出。
{:.info}

**证明** 此定理可以通过直接计算来证明，不过这里我们采用更加几何的方式，利用法曲率的几何解释来证明。

设曲面$$S$$在点$$p$$的切平面是$$\Pi$$，从$$C$$上各点向平面$$\Pi$$作垂直的投影线，这些投影线构成一个柱面记为$$\tilde{S}$$。那么曲线$$C$$是曲面$$S$$和$$\tilde{S}$$的交线，曲面$$S$$在点$$p$$的法向量$$\boldsymbol{n}$$是曲面$$\tilde{S}$$在点$$p$$的切向量。因为曲线$$C$$是曲面$$S$$和$$\tilde{S}$$的交线，所以曲线$$C$$的切向量$$\boldsymbol{e}_1$$既是曲面$$S$$的切向量，也是曲面$$\tilde{S}$$的切向量，因此

$$
\boldsymbol{e}_2 = \boldsymbol{n} \times \boldsymbol{e}_1
$$

是曲面$$\tilde{S}$$的法向量。

设曲线$$\tilde{C}$$是曲面$$\tilde{S}$$和平面$$\Pi$$的交线，它正好是曲线$$C$$在平面$$\Pi$$上的投影曲线。由于$$\boldsymbol{e}_2$$是曲面$$\tilde{S}$$的法向量，故$$\Pi$$是曲面$$\tilde{S}$$的法截面。于是，从曲面$$\tilde{S}$$上来观察，投影曲线$$\tilde{C}$$是曲面$$\tilde{S}$$上与曲线$$C$$相切的一条法截线，而且法截面$$\Pi$$的正向是由$$\boldsymbol{n}$$给出的，即从$$\boldsymbol{e}_1$$到$$\boldsymbol{e}_2$$的夹角是+90°。

设曲线$$C$$的方程是$$\boldsymbol{r} = \boldsymbol{r} (s)$$，则$$C$$作为曲面$$S$$上的曲线的测地曲率为

$$
\kappa_g = \frac{\mathrm{d}^2 \boldsymbol{r} (s)}{\mathrm{d} s^2} \cdot \boldsymbol{e}_2
$$

而从曲面$$\tilde{S}$$上来看，上式右端也是$$C$$作为曲面$$\tilde{S}$$上的曲线的法曲率$$\tilde{\kappa}_n$$，即法截线$$\tilde{C}$$作为平面$$\Pi$$上曲线的相对曲率。证毕∎

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/npQ2rvZ.png" width="80%">
</div>

**定理6.2** 曲面$$S$$的任意一条曲线$$C$$的测地曲率$$\kappa_g$$在，曲面$$S$$作保长对应时是保持不变的，即曲面上曲线的测地曲率是属于曲面内蕴几何学的量。
{:.info}

**定理6.3** 设$$(u, v)$$是曲面$$S$$上的正交参数系，因而曲面$$S$$的第一基本形式是$$\mathrm{I} = E (\mathrm{d} u)^2 + G (\mathrm{d} v)^2$$。设$$C: u = u(s), v = v(s)$$是曲面$$S$$上的一条曲线，其中$$s$$是弧长参数。假定曲线$$C$$与$$u$$-曲线的夹角是$$\theta$$，则曲线$$C$$的测地曲率是
$$
\kappa_g = \frac{\mathrm{d} \theta}{\mathrm{d} s} - \frac{1}{2 \sqrt{G}} \frac{\partial \log{E}}{\partial v} \cos{\theta} + \frac{1}{2 \sqrt{E}} \frac{\partial \log{G}}{\partial u} \sin{\theta}
$$
。
{:.info}

### 测地挠率

## 测地线

## 测地坐标系和法坐标系

## 常曲率曲面

## 曲面上切向量的平行移动

## 抽象曲面

## 抽象曲面上的几何学

## 抽象曲面的曲率

## Gauss-Bonnet公式
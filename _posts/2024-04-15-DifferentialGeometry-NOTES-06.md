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

直观上，向量$$\boldsymbol{e}_2$$是将曲线$$C$$的切向量$$\boldsymbol{e}_1 = \boldsymbol{\alpha}$$围绕曲面$$S$$的单位法向量$$\boldsymbol{n}$$按正向旋转90°得到的。与[平面曲线的Frenet标架](/2023/07/31/DifferentialGeometry-NOTES-02.html#平面曲线的frenet标架)相对照不难发现，我们在这里对于曲面$$S$$上的曲线$$C$$建立正交标架场的做法和平面曲线建立正交标架场的做法是一致的。换言之我们现在的目标是把平面上的曲线论推广成为曲面$$S$$上的曲线论。

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

**证明** 曲面$$S: \boldsymbol{r} = \boldsymbol{r} (u^1, u^2)$$上任意一条曲线$$C: u^1 = u^1 (s), u^2 = u^2 (s)$$作为空间$$\mathbb{E}^3$$中的曲线的参数方程是

$$
\boldsymbol{r} (s) = \boldsymbol{r} (u^1 (s), u^2 (s))
$$

其中$$s$$是弧长参数。所以

$$
\boldsymbol{e}_1 (s) = \boldsymbol{\alpha} (s) = \frac{\mathrm{d} \boldsymbol{r} (s)}{\mathrm{d} s} = \boldsymbol{r}_\alpha \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s}
$$

于是，根据[Gauss公式](/2023/12/27/DifferentialGeometry-NOTES-05.html#自然标架场的运动公式)有

$$
\begin{aligned}
\frac{\mathrm{d} \boldsymbol{e}_1}{\mathrm{d} s} &= \frac{\mathrm{d}^2 \boldsymbol{r} (s)}{\mathrm{d} s^2} = \boldsymbol{r}_{\alpha \beta} \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} + \boldsymbol{r}_\alpha \frac{\mathrm{d}^2 u^\alpha (s)}{\mathrm{d} s^2} \\
&= \bigg( \frac{\mathrm{d}^2 u^\gamma (s)}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^\gamma \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} \bigg) \boldsymbol{r}_\gamma + b_{\alpha \beta} \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} \boldsymbol{n}
\end{aligned}
$$

因此

$$
\begin{aligned}
\kappa_g &= \frac{\mathrm{d} \boldsymbol{e}_1 (s)}{\mathrm{d} s} \cdot \boldsymbol{e}_2 (s) \\
&= \bigg( \frac{\mathrm{d}^2 u^\gamma (s)}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^\gamma \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} \bigg) \boldsymbol{r}_\gamma \cdot \boldsymbol{e}_2
\end{aligned}
$$

但是

$$
\boldsymbol{e}_2 = \boldsymbol{n} \times \boldsymbol{e}_1 = \boldsymbol{n} \times \bigg( \frac{\mathrm{d} u^1 (s)}{\mathrm{d} s} \boldsymbol{r}_1 + \frac{\mathrm{d} u^2 (s)}{\mathrm{d} s} \boldsymbol{r}_2 \bigg)
$$

故

$$
\begin{cases}
\begin{aligned}
\boldsymbol{r}_1 \cdot \boldsymbol{e}_2 &= \frac{\mathrm{d} u^2 (s)}{\mathrm{d} s} \boldsymbol{r}_1 \cdot (\boldsymbol{n} \times \boldsymbol{r}_2) = -\frac{\mathrm{d} u^2 (s)}{\mathrm{d} s} \vert \boldsymbol{r}_1 \times \boldsymbol{r}_2 \vert \\ 
\boldsymbol{r}_2 \cdot \boldsymbol{e}_2 &= \frac{\mathrm{d} u^1 (s)}{\mathrm{d} s} \boldsymbol{r}_2 \cdot (\boldsymbol{n} \times \boldsymbol{r}_1) = \frac{\mathrm{d} u^1 (s)}{\mathrm{d} s} \vert \boldsymbol{r}_1 \times \boldsymbol{r}_2 \vert \\ 
\end{aligned}
\end{cases}
$$

因此

$$
\begin{aligned}
\kappa_g &= \vert \boldsymbol{r}_1 \times \boldsymbol{r}_2 \vert \bigg(
\frac{\mathrm{d} u^1}{\mathrm{d} s} \bigg( \frac{\mathrm{d}^2 u^2 (s)}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^2 \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg) - \frac{\mathrm{d} u^2}{\mathrm{d} s} \bigg( \frac{\mathrm{d}^2 u^1 (s)}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^1 \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg)
\bigg) \\
&= \sqrt{g_{11} g_{22} - (g_{12})^2}
\begin{vmatrix}
\frac{\mathrm{d} u^1}{\mathrm{d} s} & \frac{\mathrm{d}^2 u^1 (s)}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^1 \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \\
\frac{\mathrm{d} u^2}{\mathrm{d} s} & \frac{\mathrm{d}^2 u^2 (s)}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^2 \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \\
\end{vmatrix}
\end{aligned}
$$

由于上面的式子只依赖曲面$$S$$的第一类基本量及其导数，以及在曲面$$S$$的曲纹坐标下曲线$$C$$的参数方程及其导数，而与曲面$$S$$的第二类基本形式无关，所以当曲面$$S$$作保长变形时，曲线$$C$$的测地曲率$$\kappa_g$$是保持不变的。证毕∎

上面给出的测地曲率公式比较容易记忆，但在计算时比较复杂。如果在曲面$$S$$上取正交参数系，则曲面$$S$$上的曲线$$C$$的测地曲率$$\kappa_g$$能够写成比较简单的表达式，称为**Liouville公式**。下面我们恢复使用Gauss的记号。

**定理6.3** 设$$(u, v)$$是曲面$$S$$上的正交参数系，因而曲面$$S$$的第一基本形式是$$\mathrm{I} = E (\mathrm{d} u)^2 + G (\mathrm{d} v)^2$$。设$$C: u = u(s), v = v(s)$$是曲面$$S$$上的一条曲线，其中$$s$$是弧长参数。假定曲线$$C$$与$$u$$-曲线的夹角是$$\theta$$，则曲线$$C$$的测地曲率是
$$
\kappa_g = \frac{\mathrm{d} \theta}{\mathrm{d} s} - \frac{1}{2 \sqrt{G}} \frac{\partial \log{E}}{\partial v} \cos{\theta} + \frac{1}{2 \sqrt{E}} \frac{\partial \log{G}}{\partial u} \sin{\theta}
$$
。
{:.info}

**证明** 把$$u$$-曲线和$$v$$-曲线的单位切向量分别记成$$\boldsymbol{\alpha}_1$$和$$\boldsymbol{\alpha}_2$$，于是

$$
\begin{cases}
\begin{aligned}
\boldsymbol{\alpha}_1 &= \frac{1}{\sqrt{E}} \boldsymbol{r}_u \\
\boldsymbol{\alpha}_2 &= \frac{1}{\sqrt{E}} \boldsymbol{r}_v \\
\end{aligned}
\end{cases}
$$

因此曲线$$C$$的单位切向量能够表示成

$$
\begin{aligned}
\frac{\mathrm{d} \boldsymbol{r} (s)}{\mathrm{d} s} &= \boldsymbol{e}_1 = \cos{\theta} \boldsymbol{\alpha}_1 + \sin{\theta} \boldsymbol{\alpha}_2 \\
&= \boldsymbol{r}_u \frac{\mathrm{d} u (s)}{\mathrm{d} s} + \boldsymbol{r}_v \frac{\mathrm{d} v (s)}{\mathrm{d} s} \\
&= \sqrt{E} \frac{\mathrm{d} u (s)}{\mathrm{d} s} \boldsymbol{\alpha}_1 + \sqrt{G} \frac{\mathrm{d} v (s)}{\mathrm{d} s} \boldsymbol{\alpha}_2
\end{aligned}
$$

所以

$$
\begin{cases}
\begin{aligned}
\cos{\theta} &= \sqrt{E} \frac{\mathrm{d} u (s)}{\mathrm{d} s} \\
\sin{\theta} &= \sqrt{G} \frac{\mathrm{d} v (s)}{\mathrm{d} s} \\
\end{aligned}
\end{cases}
\Leftrightarrow
\begin{cases}
\begin{aligned}
\frac{\mathrm{d} u (s)}{\mathrm{d} s} &= \frac{1}{\sqrt{E}} \cos{\theta} \\
\frac{\mathrm{d} v (s)}{\mathrm{d} s} &= \frac{1}{\sqrt{G}} \sin{\theta} \\
\end{aligned}
\end{cases}
$$

其中$$\theta$$是$$\boldsymbol{r}' (s)$$与$$\boldsymbol{\alpha}_1$$的夹角。

因为切向量$$\boldsymbol{e}_2$$是将切向量$$\boldsymbol{e}_1$$在切平面内作正向旋转90°得到的，即$$\boldsymbol{e}_2 = \boldsymbol{n} \times \boldsymbol{e}_1$$，所以

$$
\boldsymbol{e}_2 = -\sin{\theta} \boldsymbol{\alpha}_1 + \cos{\theta} \boldsymbol{\alpha}_2
$$

但是

$$
\begin{aligned}
\frac{\mathrm{d}^2 \boldsymbol{r} (s)}{\mathrm{d} s^2} &= \frac{\mathrm{d}}{\mathrm{d} s} (\cos{\theta} \boldsymbol{\alpha}_1 + \sin{\theta} \boldsymbol{\alpha}_2) \\
&= (-\sin{\theta} \boldsymbol{\alpha}_1 + \cos{\theta} \boldsymbol{\alpha}_2) \frac{\mathrm{d} \theta}{\mathrm{d} s} + \cos{\theta} \frac{\mathrm{d} \boldsymbol{\alpha}_1}{\mathrm{d} s} + \sin{\theta} \frac{\mathrm{d} \boldsymbol{\alpha}_2}{\mathrm{d} s} \\
&= \boldsymbol{e}_2 \frac{\mathrm{d} \theta}{\mathrm{d} s} + \cos{\theta} \frac{\mathrm{d} \boldsymbol{\alpha}_1}{\mathrm{d} s} + \sin{\theta} \frac{\mathrm{d} \boldsymbol{\alpha}_2}{\mathrm{d} s}
\end{aligned}
$$

所以

$$
\kappa_g = \frac{\mathrm{d}^2 \boldsymbol{r} (s)}{\mathrm{d} s^2} \cdot \boldsymbol{e}_2 
= \frac{\mathrm{d} \theta}{\mathrm{d} s} + \cos{\theta} \frac{\mathrm{d} \boldsymbol{\alpha}_1}{\mathrm{d} s} \cdot \boldsymbol{e}_2 + \sin{\theta} \frac{\mathrm{d} \boldsymbol{\alpha}_2}{\mathrm{d} s} \cdot \boldsymbol{e}_2
$$

由于$$\boldsymbol{\alpha}_1$$和$$\boldsymbol{\alpha}_2$$是相互正交的单位向量场，有

$$
\frac{\mathrm{d} \boldsymbol{\alpha}_1}{\mathrm{d} s} \cdot \boldsymbol{\alpha}_1 = \frac{\mathrm{d} \boldsymbol{\alpha}_2}{\mathrm{d} s} \cdot \boldsymbol{\alpha}_2 = 0
$$

$$
\frac{\mathrm{d} \boldsymbol{\alpha}_1}{\mathrm{d} s} \cdot \boldsymbol{\alpha}_2 = -\frac{\mathrm{d} \boldsymbol{\alpha}_2}{\mathrm{d} s} \cdot \boldsymbol{\alpha}_1
$$

因此把$$\boldsymbol{e}_2 = -\sin{\theta} \boldsymbol{\alpha}_1 + \cos{\theta} \boldsymbol{\alpha}_2$$代入测地曲率$$\kappa_g$$的表达式可以得到

$$
\begin{aligned}
\kappa_g &= \frac{\mathrm{d} \theta}{\mathrm{d} s} + \cos{\theta} \frac{\mathrm{d} \boldsymbol{\alpha}_1}{\mathrm{d} s} \cdot \boldsymbol{e}_2 + \sin{\theta} \frac{\mathrm{d} \boldsymbol{\alpha}_2}{\mathrm{d} s} \cdot \boldsymbol{e}_2 \\
&= \frac{\mathrm{d} \theta}{\mathrm{d} s} + \cos{\theta} \frac{\mathrm{d} \boldsymbol{\alpha}_1}{\mathrm{d} s} \cdot (-\sin{\theta} \boldsymbol{\alpha}_1 + \cos{\theta} \boldsymbol{\alpha}_2) \\
&+ \sin{\theta} \frac{\mathrm{d} \boldsymbol{\alpha}_2}{\mathrm{d} s} \cdot (-\sin{\theta} \boldsymbol{\alpha}_1 + \cos{\theta} \boldsymbol{\alpha}_2) \\
&= \frac{\mathrm{d} \theta}{\mathrm{d} s} + \cos^2{\theta} \frac{\mathrm{d} \boldsymbol{\alpha}_1}{\mathrm{d} s} \cdot \boldsymbol{\alpha}_2 - \sin^2{\theta} \frac{\mathrm{d} \boldsymbol{\alpha}_2}{\mathrm{d} s} \cdot \boldsymbol{\alpha}_1 \\
&= \frac{\mathrm{d} \theta}{\mathrm{d} s} + \frac{\mathrm{d} \boldsymbol{\alpha}_1}{\mathrm{d} s} \cdot \boldsymbol{\alpha}_2
\end{aligned}
$$

由$$\boldsymbol{\alpha}_1$$和$$\boldsymbol{\alpha}_2$$的表达式得到

$$
\frac{\mathrm{d} \boldsymbol{\alpha}_1}{\mathrm{d} s} = \frac{\mathrm{d}}{\mathrm{d} s} \bigg( \frac{1}{\sqrt{E}} \bigg) \boldsymbol{r}_u + \frac{1}{\sqrt{E}} \bigg( \boldsymbol{r}_{uu} \frac{\mathrm{d} u}{\mathrm{d} s} + \boldsymbol{r}_{uv} \frac{\mathrm{d} v}{\mathrm{d} s} \bigg)
$$

$$
\frac{\mathrm{d} \boldsymbol{\alpha}_1}{\mathrm{d} s} \cdot \boldsymbol{\alpha}_2 = \frac{1}{\sqrt{EG}} \bigg( \boldsymbol{r}_{uu} \cdot \boldsymbol{r}_v \frac{\mathrm{d} u}{\mathrm{d} s} + \boldsymbol{r}_{uv} \cdot \boldsymbol{r}_v \frac{\mathrm{d} v}{\mathrm{d} s} \bigg)
$$

因为$$\boldsymbol{r}_u$$和$$\boldsymbol{r}_v$$是彼此正交的，容易得知

$$
\begin{aligned}
\boldsymbol{r}_{uu} \cdot \boldsymbol{r}_v &= (\boldsymbol{r}_u \cdot \boldsymbol{r}_v)_u - \boldsymbol{r}_u \cdot \boldsymbol{r}_{uv} = -\boldsymbol{r}_u \cdot \boldsymbol{r}_{uv} \\
&= -\frac{1}{2} \frac{\partial}{\partial v} (\boldsymbol{r}_u \cdot \boldsymbol{r}_u) = -\frac{1}{2} \frac{\partial E}{\partial v}
\end{aligned}
$$

$$
\boldsymbol{r}_{uv} \cdot \boldsymbol{r}_v = \frac{1}{2} \frac{\partial}{\partial u} (\boldsymbol{r}_v \cdot \boldsymbol{r}_v) = \frac{1}{2} \frac{\partial G}{\partial u}
$$

所以

$$
\begin{aligned}
\frac{\mathrm{d} \boldsymbol{\alpha}_1}{\mathrm{d} s} \cdot \boldsymbol{\alpha}_2 &= \frac{1}{\sqrt{EG}} \bigg( -\frac{1}{2} \frac{\partial E}{\partial v} \cdot \frac{\mathrm{d} u}{\mathrm{d} s} + \frac{1}{2} \frac{\partial G}{\partial u} \cdot \frac{\mathrm{d} v}{\mathrm{d} s} \bigg)\\
&= \frac{1}{\sqrt{EG}} \bigg( -\frac{1}{2 \sqrt{E}} \frac{\partial E}{\partial v} \cos{\theta} + \frac{1}{2 \sqrt{G}} \frac{\partial G}{\partial u} \sin{\theta} \bigg) \\
&= -\frac{1}{2 \sqrt{G}} \frac{\partial \log{E}}{\partial v} \cos{\theta} + \frac{1}{2 \sqrt{E}} \frac{\partial \log{G}}{\partial u} \sin{\theta}
\end{aligned}
$$

因此

$$
\kappa_g = \frac{\mathrm{d} \theta}{\mathrm{d} s} - \frac{1}{2 \sqrt{G}} \frac{\partial \log{E}}{\partial v} \cos{\theta} + \frac{1}{2 \sqrt{E}} \frac{\partial \log{G}}{\partial u} \sin{\theta}
$$

证毕∎

作为特例，考虑$$u$$-曲线的测地曲率$$\kappa_{g1}$$。此时$$\theta = 0$$，因此

$$
\kappa_{g1} = -\frac{1}{2 \sqrt{G}} \frac{\partial \log{E}}{\partial v}
$$

同时，对于$$v$$-曲线，$$\theta = \frac{\pi}{2}$$，因此它的测地曲率$$\kappa_{g2}$$是

$$
\kappa_{g2} = \frac{1}{2 \sqrt{E}} \frac{\partial \log{G}}{\partial u}
$$

这样，Liouville公式又可以写成

$$
\kappa_g = \frac{\mathrm{d} \theta}{\mathrm{d} s} + \kappa_{g1} \cos{\theta} + \kappa_{g2} \sin{\theta}
$$

### 测地挠率

最后，我们来讨论测地挠率。由[自然标架的运动公式](/2023/12/27/DifferentialGeometry-NOTES-05.html#自然标架场的运动公式)得到

$$
\frac{\mathrm{d} \boldsymbol{n} (s)}{\mathrm{d} s} = \frac{\partial \boldsymbol{n}}{\partial u^\alpha} \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} = -b_\alpha^\beta \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \boldsymbol{r}_\beta
$$

代入测地挠率$$\tau_g$$的表达式得到

$$
\begin{aligned}
\tau_g &= \big( \boldsymbol{n}, \boldsymbol{n}' (s), \boldsymbol{r}' (s) \big) = -b_\alpha^\beta \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \big( \boldsymbol{n}, \boldsymbol{r}_\beta, \boldsymbol{r}_\gamma \big) \\
&= \bigg( -b_\alpha^1 \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^2}{\mathrm{d} s} + b_\alpha^2 \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^1}{\mathrm{d} s} \bigg) \vert \boldsymbol{r}_1 \times \boldsymbol{r}_2 \vert \\
&= \sqrt{g} \bigg( -b_2^1 \bigg( \frac{\mathrm{d} u^2}{\mathrm{d} s} \bigg)^2 + (b_2^2 - b_1^1) \frac{\mathrm{d} u^1}{\mathrm{d} s} \frac{\mathrm{d} u^2}{\mathrm{d} s} + b_1^1 \bigg( \frac{\mathrm{d} u^1}{\mathrm{d} s} \bigg)^2 \bigg)
\end{aligned}
$$

由于

$$
g^{11} = \frac{g_{22}}{g}, \ \ \ g^{12} = g^{21} = -\frac{g_{12}}{g}, \ \ \ g^{22} = \frac{g_{11}}{g}
$$

所以

$$
-b_2^1 = -g^{11} b_{12} - g^{12} b_{22} = \frac{1}{g} 
\begin{vmatrix}
g_{12} & g_{22} \\ b_{12} & b_{22}
\end{vmatrix}
$$

$$
b_2^2 - b_1^1 = g^{21} b_{12} + g^{22} b_{22} - g^{11} b_{11} - g^{12} b_{21} = \frac{1}{g}
\begin{vmatrix}
g_{11} & g_{22} \\ b_{11} & b_{22}
\end{vmatrix}
$$

$$
b_1^2 = g^{21} b_{11} + g^{22} b_{21} = \frac{1}{g}
\begin{vmatrix}
g_{11} & g_{12} \\ b_{11} & b_{12}
\end{vmatrix}
$$

因此

$$
\tau_g = \frac{1}{\sqrt{g}}
\begin{vmatrix}
\bigg( \frac{\mathrm{d} u^2}{\mathrm{d} s} \bigg)^2 & \frac{\mathrm{d} u^1}{\mathrm{d} s} \frac{\mathrm{d} u^2}{\mathrm{d} s} & \bigg( \frac{\mathrm{d} u^1}{\mathrm{d} s} \bigg)^2 \\
g_{11} & g_{12} & g_{22} \\
b_{11} & b_{12} & b_{22} \\
\end{vmatrix}
$$

从测地挠率的表达式可以看出，曲面$$S$$上的曲线$$C$$的测地挠率$$\tau_g$$和法曲率一样，只是曲面$$S$$上的切方向的函数，反映的是曲面$$S$$本身的性质，而不只是曲面$$S$$上的曲线$$C$$的性质。特别是，如果曲面$$S$$上有两条在一点相切的曲线，则这两条曲线在该点有相同的测地挠率。很明显，测地挠率$$\tau_g$$**不是**曲面$$S$$的内蕴几何量。

与[曲率线所满足的微分方程](/2023/11/10/DifferentialGeometry-NOTES-04.html#平均曲率和gauss曲率)相对照不难发现，主方向恰好是曲面上使测地挠率为零的切方向。因此，曲面上的曲率线正好是沿其切方向的测地挠率为零的曲线。换言之，曲率线的微分方程是$$\tau_g = 0$$。实际上可以证明切平面上与主方向$$\boldsymbol{e}_1$$成$$\theta$$角度的切方向的测地曲率是

$$
\tau_g = \frac{1}{2} (\kappa_2 - \kappa_1) \sin{2 \theta} = \frac{1}{2} \frac{\mathrm{d} \kappa_n (\theta)}{\mathrm{d} \theta}
$$

因此$$\kappa_g$$取极值的方向(即曲面的主方向)恰好是$$\tau_g$$取零值的方向。

**定理6.4** 在曲面$$S$$上非直线的渐近曲线$$C$$的挠率是曲面$$S$$沿曲线$$C$$的切方向的测地挠率。
{:.info}

**证明** 由于曲线$$C$$是非直线的渐近曲线，故$$\kappa \neq 0$$，但是$$\kappa_n \equiv 0$$。于是标架场的运动方程成为

$$
\begin{cases}
\begin{aligned}
\frac{\mathrm{d} \boldsymbol{r} (s)}{\mathrm{d} s} &= \boldsymbol{e}_1 \\
\frac{\mathrm{d} \boldsymbol{e}_1}{\mathrm{d} s} &= \vert \kappa_g \vert (\varepsilon \boldsymbol{e}_2) \\
\frac{\mathrm{d} (\varepsilon \boldsymbol{e}_2)}{\mathrm{d} s} &= -\vert \kappa_g \vert \boldsymbol{e}_1 + \tau_g (\varepsilon \boldsymbol{e}_3) \\
\frac{\mathrm{d} (\varepsilon \boldsymbol{e}_3)}{\mathrm{d} s} &= - \tau_g (\varepsilon \boldsymbol{e}_2)\\
\end{aligned}
\end{cases}
$$

因为

$$
\kappa_g^2 = \kappa_g^2 + \kappa_n^2 = \kappa^2 \neq 0
$$

所以$$\{ \boldsymbol{r} (s); \boldsymbol{e}_1, \varepsilon \boldsymbol{e}_2, \varepsilon \boldsymbol{e}_3 \}$$恰好是曲线$$C$$的Frenet标架，其中$$\varepsilon = \text{sign} (\kappa_g)$$。因此曲线$$C$$的曲率是$$\vert \kappa_g \vert$$，挠率是$$\tau_g$$。证毕∎

总起来说，本节介绍了曲面$$S$$上的曲线C的测地曲率和测地挠率的概念，其中测地曲率是曲面$$S$$的内蕴几何量，与曲面$$S$$的第二基本形式无关；测地挠率是曲面$$S$$在任意一点的切方向的函数，它与法曲率有密切的关系，实际上测地挠率是法曲率作为切方向的函数的导数之半。

从方法上来讲，沿曲面$$S$$上的曲线$$C$$建立与曲面$$S$$和曲线$$C$$都有关联的单位正交标架场是十分重要的。实际上，这是把平面上曲线的Frenet标架场搬到曲面上的情形。测地曲率的Liouville公式是十分有用的，它的推导过程有典型意义，应该予以足够的重视。

## 测地线

曲面$$S$$上的法曲率和测地挠率不是曲面$$S$$的内蕴几何量，因此渐近曲线和曲率线也都不属于曲面的内蕴几何的概念。曲面$$S$$上曲线$$C$$的测地曲率和它们不一样，当曲面$$S$$作保长变形时，曲线$$C$$的测地曲率是保持不变的。由此可见，曲面$$S$$上曲线$$C$$的测地曲率是内蕴几何量，因此曲面$$S$$上测地曲率为零的曲线，即测地线，属于曲面的内蕴几何学研究的内容。在本节，我们要研究曲面上的测地线的特征和性质，既要从曲面的外在几何的角度来观测，更要从曲面内蕴几何的角度进行研究。

**定义6.1** 在曲面$$S$$上测地曲率恒等于零的曲线称为曲面$$S$$上的**测地线**。
{:.success}

很明显，平面曲线的测地曲率就是它的相对曲率，因此平面上的测地线就是该平面上的直线。由此可见，曲面上的测地线的概念是平面上的直线概念的推广。在本节我们将从各个方面来解释这种推广的含义。

**定理6.5** 曲面$$S$$上的一条曲线$$C$$是测地线，当且仅当它或者是一条直线，或者它的主法向量处处是曲面$$S$$的法向量。
{:.info}

**证明** 在上一节已经知道曲面$$S$$上的曲线$$C$$的测地曲率是

$$
\kappa_g = \kappa \cos{\tilde{\theta}}
$$

其中$$\tilde{\theta}$$是曲线$$C$$的次法向量和曲面$$S$$的法向量的夹角。当$$C$$是曲面$$S$$上的测地线时，$$\kappa_g \equiv 0$$，所以在曲线$$C$$的每一点必须有$$\kappa = 0$$或者$$\cos{\tilde{\theta}} = 0$$。如果在曲线$$C$$上处处有$$\kappa = 0$$，则该曲线$$C$$是一条直线；如果在曲线$$C$$的点$$p$$处$$\kappa (p) \neq 0$$，则由曲率函数的连续性得知在点$$p$$的一个邻域内处处有$$\kappa \neq 0$$，于是$$\cos{\tilde{\theta}} \equiv 0$$，因此$$\tilde{\theta} = \frac{\pi}{2}$$，即曲线$$C$$的次法向量和曲面$$S$$的法向量垂直，这就是说，曲线$$C$$的主法向量是曲面$$S$$的法向量。反过来是明显的。证毕∎

### 测地线方程

为了在一般的曲面$$S$$上求测地线，需要知道曲面$$S$$上的测地线所满足的微分方程。在上一节我们推导过切向量$$\boldsymbol{e}_1$$的运动方程

$$
\begin{aligned}
\frac{\mathrm{d} \boldsymbol{e}_1 (s)}{\mathrm{d} s} &= \kappa_g \boldsymbol{e}_2 + \kappa_n \boldsymbol{e}_3 \\
&= \frac{\mathrm{d}^2 \boldsymbol{r} (s)}{\mathrm{d} s^2} = \boldsymbol{r}_{\alpha \beta} \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} + \boldsymbol{r}_\alpha \frac{\mathrm{d}^2 u^\alpha (s)}{\mathrm{d} s^2} \\
&= \bigg( \frac{\mathrm{d}^2 u^\gamma (s)}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^\gamma \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} \bigg) \boldsymbol{r}_\gamma + b_{\alpha \beta} \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} \boldsymbol{e}_3
\end{aligned}
$$

因此

$$
\kappa_g \boldsymbol{e}_2 = \bigg( \frac{\mathrm{d}^2 u^\gamma (s)}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^\gamma \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} \bigg) \boldsymbol{r}_\gamma
$$

显然$$\boldsymbol{r}_1$$和$$\boldsymbol{r}_2$$是线性无关的，因此$$\kappa_g \equiv 0$$的充分必要条件是

$$
\frac{\mathrm{d}^2 u^\gamma (s)}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^\gamma \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} = 0
$$

这就是曲面$$S$$上的测地线所满足的微分方程，并且该方程只涉及曲面$$S$$的第一基本形式，而与曲面$$S$$的第二基本形式无关。因此，这是曲面$$S$$上的测地线属于曲面内蕴几何范畴的微分方程。

若引进新的未知函数$$v^\gamma$$，则上面的二阶常微分方程组便降阶为一阶常微分方程组

$$
\begin{cases}
\begin{aligned}
\frac{\mathrm{d} u^\gamma}{\mathrm{d} s} &= v^\gamma \\
\frac{\mathrm{d} v^\gamma}{\mathrm{d} s} &= -\Gamma_{\alpha \beta}^\gamma v^\alpha v^\beta
\end{aligned}
\end{cases}
$$

这是拟线性常微分方程组。根据常微分方程组的理论，对于任意给定的初始值$$(u_0^1, u_0^2; v_0^1, v_0^2)$$，必存在$$\varepsilon \gt 0$$，使得方程组有定义在区间$$(-\varepsilon, \varepsilon)$$上的唯一解$$u^\gamma = u^\gamma (s)$$，$$v^\gamma = v^\gamma (s)$$，满足初始条件

$$
u^\gamma (0) = u_0^\gamma, \ \ \ v^\gamma (0) = v_0^\gamma
$$

很明显，函数组$$u^\gamma = u^\gamma (s)$$满足测地线的微分方程组。

如果初始值$$(u_0^1, u_0^2; v_0^1, v_0^2)$$满足条件

$$
g_{\alpha \beta} (u_0^1, u_0^2) v_0^\alpha v_0^\beta = 1
$$

则能够证明如上所给出的解函数$$u^\gamma = u^\gamma (s)$$是曲面$$S$$上以弧长$$s$$为参数的一条测地线。实际上，如果命

$$
f(s) = g_{\alpha \beta} (u^1 (s), u^2 (s)) \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} - 1
$$

则

$$
\begin{aligned}
\frac{\mathrm{d} f (s)}{\mathrm{d} s} &= \frac{\partial g_{\alpha \beta}}{\partial u^\gamma} \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} + 2 g_{\alpha \beta} \frac{\mathrm{d}^2 u^\alpha}{\mathrm{d} s^2} \frac{\mathrm{d}^2 u^\beta}{\mathrm{d} s^2} \\
&= (\Gamma_{\alpha \beta \gamma} + \Gamma_{\beta \alpha \gamma}) \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} - 2 g_{\alpha \beta} \Gamma_{\gamma \delta}^\alpha \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\delta}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} = 0
\end{aligned}
$$

根据条件$$f(0) = g_{\alpha \beta} (u_0^1, u_0^2) v_0^\alpha v_0^\beta - 1 = 0$$，所以

$$
f (s) \equiv 0
$$

这意味着，由方程$$u^\gamma = u^\gamma (s)$$给出的曲线是正则曲线，并且$$s$$是它的弧长参数。上面的讨论可以归结为

**定理6.6** 对于曲面$$S$$上的任意一点$$p$$和曲面$$S$$在点$$p$$的任意一个单位切向量$$\boldsymbol{v}$$，在曲面$$S$$上必存在唯一的一条以弧长为参数的测地线$$C$$通过点$$p$$，并且在点$$p$$以$$\boldsymbol{v}$$为它的切向量。
{:.info}

需要指出，**定理6.6**的证明本身说明方程组

$$
\frac{\mathrm{d}^2 u^\gamma (s)}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^\gamma \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} = 0
$$

的解$$u = u^\gamma (s)$$必定满足

$$
\frac{\mathrm{d}}{\mathrm{d} s} \bigg( g_{\alpha \beta} (u^1 (s), u^2 (s)) \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} \bigg) = 0
$$

因此只要初始值$$(v_0^1, v_0^2) \neq \mathbf{0}$$，则

$$
\begin{aligned}
\bigg\vert \frac{\mathrm{d} \boldsymbol{r} (s)}{\mathrm{d} s} \bigg\vert^2 &= g_{\alpha \beta} (u^1 (s), u^2 (s)) \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} \\
&= g_{\alpha \beta} (u_0^1, u_0^2) v_0^\alpha v_0^\beta = \text{常数} \neq 0
\end{aligned}
$$

这就是说，曲线$$C: \boldsymbol{r} = \boldsymbol{r} (u^1 (s), u^2 (s))$$是正则曲线，并且参数$$s$$与弧长成比例。特别是，当条件

$$
u^\gamma (0) = u_0^\gamma, \ \ \ v^\gamma (0) = v_0^\gamma
$$

成立时，即切向量$$\boldsymbol{v}$$的长度为1时，$$s$$恰好是它的弧长参数。

如果在曲面$$S$$上取正交参数系$$(u, v)$$，则利用测地曲率的Liouville公式，测地线的微分方程组还可以写成

$$
\begin{cases}
\begin{aligned}
\frac{\mathrm{d} u}{\mathrm{d} s} &= \frac{1}{\sqrt{E}} \cos{\theta} \\
\frac{\mathrm{d} v}{\mathrm{d} s} &= \frac{1}{\sqrt{G}} \sin{\theta} \\
\frac{\mathrm{d} \theta}{\mathrm{d} s} &= \frac{1}{2 \sqrt{G}} \frac{\partial \log{E}}{\partial v} \cos{\theta} - \frac{1}{2 \sqrt{E}} \frac{\partial \log{G}}{\partial u} \sin{\theta}
\end{aligned}
\end{cases}
$$

### 曲面上的最短线

众所周知，在平面上连接两点的最短线是以这两点为端点的直线段。在曲面上，测地线具有类似的性质。下面先简要地介绍曲面$$S$$上的曲线$$C$$的变分的概念。

设$$C: u^\alpha = u^\alpha (s), \alpha = 1, 2$$是曲面$$S: \boldsymbol{r} = \boldsymbol{r} (u^1, u^2)$$上的一条曲线，其中$$a \leq s \leq b$$，且$$s$$是曲线$$C$$的弧长参数。如果存在定义在区域$$[a, b] \times (-\varepsilon, \varepsilon)$$上的可微函数

$$
u^\alpha = u^\alpha (s, t)
$$

使得

$$
u^\alpha (s, 0) = u^\alpha (s)
$$

则称$$u^\alpha = u^\alpha (s, t)$$是曲线$$C$$的一个**变分**。如果进一步有

$$
u^\alpha (a, t) = u^\alpha (a), \ \ \ u^\alpha (b, t) = u^\alpha (b)
$$

则称该变分有固定的端点。在直观上，对于每一个参数$$t \in (-\varepsilon, \varepsilon)$$，函数组$$u^\alpha (s, t)$$给出了一条曲线$$C_t$$，它的参数方程是

$$
u^\alpha = u_t^\alpha (s) = u^\alpha (s, t)
$$

条件$$u^\alpha (s, 0) = u^\alpha (s)$$说明已知的曲线$$C$$是这族曲线中的一员，且$$C = C_0$$。因此，所谓的曲线$$C$$的变分就是把它嵌入到在它周围变化的一个曲线族$$C_t$$中去。有固定端点的意思是，曲线$$C$$的变分曲线$$C_t$$和曲线$$C$$本身有相同的起点和终点，即它们有公共的端点。需要指出的是，尽管可以假定参数$$s$$是曲线$$C$$的弧长参数，但是$$s$$未必是变分曲线$$C_t$$的弧长参数。

用$$L(C)$$表示曲线$$C$$的长度，即

$$
L(C) = \int_a^b \sqrt{g_{\alpha \beta} (u^1 (s), u^2 (s)) \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s}} \ \mathrm{d} s
$$

曲线$$C$$是连接它的两个端点的最短线的意思是，它的长度不会比连接曲线$$C$$的端点的其他曲线的长度更长。特别是，如果把曲线$$C$$嵌入到任意一个有相同端点的变分曲线族$$C_t$$中时，必定有$$L(C) \leq L(C_t)$$，于是应该有

$$
\frac{\mathrm{d}}{\mathrm{d} t} \bigg\vert_{t = 0} L(C_t) = 0
$$

当曲面$$S$$上的曲线$$C$$关于它的一个变分$$C_t$$满足上述条件，则称曲线$$C$$的弧长在它的变分曲线$$C_t$$中达到临界值。需要指出的是，上面的做法完全忽略了曲面$$S$$的外在特征，而只与曲面$$S$$的第一基本形式有关，这就是说，上述考虑属于曲面$$S$$的内蕴几何的范畴。

命

$$
v^\alpha (s) = \frac{\partial}{\partial t} \bigg\vert_{t = 0} u^\alpha (s, t)
$$

$$
\boldsymbol{v} (s) = v^\alpha \boldsymbol{r}_\alpha (u^1 (s), u^2 (s))
$$

则$$\boldsymbol{v} (s)$$是曲面$$S$$上沿曲线$$C$$定义的一个切向量场，称为变分$$u^\alpha (s, t)$$的**变分向量场**。实际上，变分向量$$\boldsymbol{v} (s_0)$$是变分$$u^\alpha (s, t)$$在$$s = s_0$$时给出的曲线$$u^\alpha = u^\alpha (s_0, t)$$在$$t = 0$$处的切向量。条件$$u^\alpha (a, t) = u^\alpha (a)， u^\alpha (b, t) = u^\alpha (b)$$意味着$$\boldsymbol{v} (a) = \boldsymbol{0}$$，$$\boldsymbol{v} (b) = \boldsymbol{0}$$，即对于曲线$$C$$有固定端点的变分而言，它的变分向量场在端点的值为零。反过来，如果在曲面$$S$$上沿曲线$$C$$给定了一个切向量场$$\boldsymbol{v} (s)$$，则可以定义曲线$$C$$的一个变分，使得它的变分向量场是$$\boldsymbol{v} (s)$$。实际上，只要命

$$
u^\alpha (s, t) = u^\alpha (s) + t v^\alpha (s)
$$

就可以了。很明显，当$$\boldsymbol{v} (a) = \boldsymbol{0}$$，$$\boldsymbol{v} (b) = \boldsymbol{0}$$时，上面的变分确实有固定的端点。

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/FSM2GOh.png" width="80%">
</div>

假定曲面$$S$$的第一基本形式是

$$
\mathrm{I} = g_{\alpha \beta} (u^1, u^2) \mathrm{d} u^\alpha \mathrm{d} u^\beta
$$

则变分曲线$$C_t$$的长度是

$$
L(C_t) = \int_a^b \sqrt{g_{\alpha \beta} (u^1 (s), u^2 (s)) \frac{\partial u^\alpha (s, t)}{\partial s} \frac{\partial u^\beta (s, t)}{\partial s}} \ \mathrm{d} s
$$

所以

$$
\begin{aligned}
\frac{\mathrm{d}}{\mathrm{d} t} L(C_t) &= \int_a^b \frac{\partial}{\partial t} \bigg( \sqrt{g_{\alpha \beta} \frac{\partial u^\alpha}{\partial s} \frac{\partial u^\beta}{\partial s}} \bigg) \ \mathrm{d} s \\
&= \frac{1}{2} \int_a^b \bigg( \frac{\partial g_{\alpha \beta}}{\partial u^\gamma} \frac{\partial u^\gamma}{\partial t} \frac{\partial u^\alpha}{\partial s} \frac{\partial u^\beta}{\partial s} + 2 g_{\alpha \beta} \frac{\partial^2 u^\alpha}{\partial s \partial t} \frac{\partial u^\beta}{\partial s} \bigg) \\
&\cdot \bigg( g_{\alpha \beta} \frac{\partial u^\alpha}{\partial s} \frac{\partial u^\beta}{\partial s} \bigg)^{-\frac{1}{2}} \ \mathrm{d} s
\end{aligned}
$$

因为$$s$$是曲线$$C = C_0$$的弧长参数，因此

$$
g_{\alpha \beta} \frac{\partial u^\alpha}{\partial s} \frac{\partial u^\beta}{\partial s} \bigg\vert_{t=0} = 1
$$

所以

$$
\frac{\mathrm{d}}{\mathrm{d} t} L(C_t) \bigg\vert_{t=0} = \int_a^b \frac{1}{2} \bigg( \frac{\partial g_{\alpha \beta}}{\partial u^\gamma} v^\gamma (s) \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} + 2 g_{\alpha \beta} \frac{\mathrm{d} v^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg) \ \mathrm{d} s
$$

由于

$$
\begin{aligned}
g_{\alpha \beta} \frac{\mathrm{d} v^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} &= \frac{\mathrm{d}}{\mathrm{d} s} \bigg( g_{\alpha \beta} v^\alpha \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg) - v^\alpha \frac{\mathrm{d}}{\mathrm{d} s} \bigg( g_{\alpha \beta} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg) \\
&= \frac{\mathrm{d}}{\mathrm{d} s} \bigg( g_{\alpha \beta} v^\alpha \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg) - v^\alpha \bigg( \frac{\partial g_{\alpha \beta}}{\partial u^\gamma} \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} + g_{\alpha \beta} \frac{\mathrm{d}^2 u^\beta}{\mathrm{d} s^2} \bigg)
\end{aligned}
$$

代入前面的式子后再用分部积分得到

$$
\begin{aligned}
\frac{\mathrm{d}}{\mathrm{d} t} L(C_t) \bigg\vert_{t=0} &= \int_a^b \bigg[ \frac{\mathrm{d}}{\mathrm{d} s} \bigg( g_{\alpha \beta} v^\alpha \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg) - v^\alpha \bigg(
  g_{\alpha \beta} \frac{\mathrm{d}^2 u^\beta}{\mathrm{d} s^2} 
  + \frac{1}{2} \bigg( 
  \frac{\partial g_{\alpha \beta}}{\partial u^\gamma} + \frac{\partial g_{\alpha \gamma}}{\partial u^\beta} - \frac{\partial g_{\gamma \beta}}{\partial u^\alpha}
  \bigg)
  \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} 
\bigg) \bigg] \ \mathrm{d} s \\
&= g_{\alpha \beta} v^\alpha \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg\vert_{s = a}^{s = b} - \int_a^b g_{\alpha \beta} v^\alpha \bigg( \frac{\mathrm{d}^2 u^\beta}{\mathrm{d} s^2} +\Gamma_{\gamma \delta}^\beta \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\delta}{\mathrm{d} s} \bigg) \ \mathrm{d} s
\end{aligned}
$$

假定变分有固定的端点，则$$v^\alpha (a) = b^\alpha (b) = 0$$，于是

$$
\frac{\mathrm{d}}{\mathrm{d} t} L(C_t) \bigg\vert_{t=0} = -\int_a^b g_{\alpha \beta} v^\alpha \bigg( \frac{\mathrm{d}^2 u^\beta}{\mathrm{d} s^2} +\Gamma_{\gamma \delta}^\beta \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\delta}{\mathrm{d} s} \bigg) \ \mathrm{d} s
$$

前一个关于$$\frac{\mathrm{d}}{\mathrm{d} t} L(C_t) \bigg\vert_{t=0}$$的式子称为曲面$$S$$上的曲线$$C$$的弧长的第一变分公式，而后一个式子称为曲面$$S$$上的曲线$$C$$关于有固定端点的变分的弧长的第一变分公式。

**定理6.7** 设$$C$$是曲面$$S$$上的一条曲线，则$$C$$的弧长在它的任意一个有固定端点的变分$$C_t$$中达到临界值的充分必要条件是，曲线$$C$$是曲面$$S$$上的测地线。
{:.info}

**证明** 设$$C$$是曲面$$S$$上的一条测地线，则它的参数方程$$u^\alpha = u^\alpha (s)$$满足微分方程组

$$
\frac{\mathrm{d}^2 u^\beta}{\mathrm{d} s^2} + \Gamma_{\gamma \delta}^\beta \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\delta}{\mathrm{d} s} = 0
$$

于是根据第一变分公式，对于曲线$$C$$的任意一个有固定端点的变分$$C_t$$有下式成立

$$
\frac{\mathrm{d}}{\mathrm{d} t} L(C_t) \bigg\vert_{t = 0} = 0
$$

反过来，假定对于曲线$$C$$的任意一个有固定端点的变分$$C_t$$，上式都成立。取

$$
v^\alpha (s) = \sin{\frac{(s - a) \pi}{b-a}} \bigg( \frac{\mathrm{d}^2 u^\alpha}{\mathrm{d} s^2} + \Gamma_{\xi \eta}^\alpha \frac{\mathrm{d} u^\xi}{\mathrm{d} s} \frac{\mathrm{d} u^\eta}{\mathrm{d} s} \bigg)
$$

则$$v^\alpha (a) = v^\alpha (b) = 0$$，于是在曲面$$S$$上有曲线$$C$$的以$$v^\alpha (a)$$为变分向量场的变分$$C_t$$，它有固定的端点。将上式代入有固定端点的变分的弧长的第一变分公式得到

$$
\begin{aligned}
\frac{\mathrm{d}}{\mathrm{d} t} L(C_t) \bigg\vert_{t=0} &= \int_a^b \sin{\frac{(s - a) \pi}{b-a}} g_{\alpha \beta} \bigg( \frac{\mathrm{d}^2 u^\alpha}{\mathrm{d} s^2} + \Gamma_{\xi \eta}^\alpha \frac{\mathrm{d} u^\xi}{\mathrm{d} s} \frac{\mathrm{d} u^\eta}{\mathrm{d} s} \bigg)\\
&\cdot \bigg( \frac{\mathrm{d}^2 u^\beta}{\mathrm{d} s^2} +\Gamma_{\gamma \delta}^\beta \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\delta}{\mathrm{d} s} \bigg) \ \mathrm{d} s
\end{aligned}
$$

根据关系式

$$
\kappa_g \boldsymbol{e}_2 = \bigg( \frac{\mathrm{d}^2 u^\gamma}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^\gamma \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg) \boldsymbol{r}_\gamma
$$

有

$$
\begin{aligned}
(\kappa_g)^2 &= (\kappa_g \boldsymbol{e}_2) \cdot (\kappa_g \boldsymbol{e}_2) \\
&= \bigg( \frac{\mathrm{d}^2 u^\alpha}{\mathrm{d} s^2} + \Gamma_{\xi \eta}^\alpha \frac{\mathrm{d} u^\xi}{\mathrm{d} s} \frac{\mathrm{d} u^\eta}{\mathrm{d} s} \bigg) \bigg( \frac{\mathrm{d}^2 u^\beta}{\mathrm{d} s^2} +\Gamma_{\gamma \delta}^\beta \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\delta}{\mathrm{d} s} \bigg)\boldsymbol{r}_\alpha \cdot \boldsymbol{r}_\beta \\
&= g_{\alpha \beta} \bigg( \frac{\mathrm{d}^2 u^\alpha}{\mathrm{d} s^2} + \Gamma_{\xi \eta}^\alpha \frac{\mathrm{d} u^\xi}{\mathrm{d} s} \frac{\mathrm{d} u^\eta}{\mathrm{d} s} \bigg) \bigg( \frac{\mathrm{d}^2 u^\beta}{\mathrm{d} s^2} +\Gamma_{\gamma \delta}^\beta \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\delta}{\mathrm{d} s} \bigg)
\end{aligned}
$$

因此

$$
\frac{\mathrm{d}}{\mathrm{d} t} L(C_t) \bigg\vert_{t = 0} = \int_a^b \sin{\frac{(s - a) \pi}{b-a}} (\kappa_g)^2 \ \mathrm{d} s = 0
$$

由于上式的被积表达式$$\sin{\frac{(s - a) \pi}{b-a}} (\kappa_g)^2 \geq 0$$，故有

$$
\sin{\frac{(s - a) \pi}{b-a}} (\kappa_g)^2 = 0
$$

于是$$\kappa_g \equiv 0$$，曲线$$C$$是曲面$$S$$上的测地线。证毕∎

**推论** 设$$p$$，$$q$$是曲面$$S$$上的任意两点，如果曲线$$C$$是在曲面$$S$$上连接$$p$$，$$q$$两点的最短线，则$$C$$必是曲面$$S$$上的测地线。
{:.info}

**定理6.7**的证明过程只涉及曲面$$S$$的第一基本形式，与曲面$$S$$的外在特征无关。

## 测地坐标系和法坐标系

## 常曲率曲面

## 曲面上切向量的平行移动

## 抽象曲面

## 抽象曲面上的几何学

## 抽象曲面的曲率

## Gauss-Bonnet公式
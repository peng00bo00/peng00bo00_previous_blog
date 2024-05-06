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

所以$$\kappa_n$$恰好是曲面$$S$$沿曲线$$C$$的切方向的[法曲率](/2023/11/10/DifferentialGeometry-NOTES-04.html#法曲率)。类似地，将运动方程的第二式两边同时和$$\boldsymbol{e}_2$$作内积得到

$$
\kappa_g = \frac{\mathrm{d}^2 \boldsymbol{r} (s)}{\mathrm{d} s^2} \cdot \boldsymbol{e}_2 = \boldsymbol{r}'' (s) \cdot (\boldsymbol{n} (s) \times \boldsymbol{r}' (s)) = \big( \boldsymbol{n} (s), \boldsymbol{r}' (s), \boldsymbol{r}'' (s) \big)
$$

称$$\kappa_g$$为曲面$$S$$上的曲线$$C$$的**测地曲率**。另外

$$
\begin{aligned}
\tau_g &= \frac{\mathrm{d} \boldsymbol{e}_2}{\mathrm{d} s} \cdot \boldsymbol{n} = \frac{\mathrm{d} (\boldsymbol{n} \times \boldsymbol{r}' (s))}{\mathrm{d} s} \cdot \boldsymbol{n} \\
&= (\boldsymbol{n}' (s) \times \boldsymbol{r}' (s)) \cdot \boldsymbol{n} = \big( \boldsymbol{n} (s), \boldsymbol{n}' (s), \boldsymbol{r}' (s) \big)
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

**定理6.2** 曲面$$S$$上的任意一条曲线$$C$$的测地曲率$$\kappa_g$$在曲面$$S$$作保长对应时是保持不变的，即曲面上曲线的测地曲率是属于曲面内蕴几何学的量。
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
\frac{\mathrm{d} \boldsymbol{e}_1 (s)}{\mathrm{d} s} &= \frac{\mathrm{d}^2 \boldsymbol{r} (s)}{\mathrm{d} s^2} = \boldsymbol{r}_{\alpha \beta} \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} + \boldsymbol{r}_\alpha \frac{\mathrm{d}^2 u^\alpha (s)}{\mathrm{d} s^2} \\
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
\frac{\mathrm{d} u^1}{\mathrm{d} s} \bigg( \frac{\mathrm{d}^2 u^2}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^2 \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg) - \frac{\mathrm{d} u^2}{\mathrm{d} s} \bigg( \frac{\mathrm{d}^2 u^1}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^1 \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg)
\bigg) \\
&= \sqrt{g_{11} g_{22} - (g_{12})^2}
\begin{vmatrix}
\frac{\mathrm{d} u^1}{\mathrm{d} s} & \frac{\mathrm{d}^2 u^1 (s)}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^1 \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \\
\frac{\mathrm{d} u^2}{\mathrm{d} s} & \frac{\mathrm{d}^2 u^2 (s)}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^2 \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \\
\end{vmatrix}
\end{aligned}
$$

由于上面的式子只依赖曲面$$S$$的第一类基本量及其导数，以及在曲面$$S$$的曲纹坐标下曲线$$C$$的参数方程及其导数，而与曲面$$S$$的第二类基本形式无关，所以当曲面$$S$$作保长变形时，曲线$$C$$的测地曲率$$\kappa_g$$是保持不变的。证毕∎

上面给出的测地曲率公式比较容易记忆，但是在计算时比较复杂。如果在曲面$$S$$上取正交参数系，则曲面$$S$$上的曲线$$C$$的测地曲率$$\kappa_g$$能够写成比较简单的表达式，称为**Liouville公式**。下面我们恢复使用Gauss的记号。

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
\tau_g &= \big( \boldsymbol{n} (s), \boldsymbol{n}' (s), \boldsymbol{r}' (s) \big) = -b_\alpha^\beta \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \big( \boldsymbol{n}, \boldsymbol{r}_\beta, \boldsymbol{r}_\gamma \big) \\
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
\bigg( \frac{\mathrm{d} u^2}{\mathrm{d} s} \bigg)^2 & -\frac{\mathrm{d} u^1}{\mathrm{d} s} \frac{\mathrm{d} u^2}{\mathrm{d} s} & \bigg( \frac{\mathrm{d} u^1}{\mathrm{d} s} \bigg)^2 \\
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

总起来说，本节介绍了曲面$$S$$上的曲线$$C$$的测地曲率和测地挠率的概念，其中测地曲率是曲面$$S$$的内蕴几何量，与曲面$$S$$的第二基本形式无关；测地挠率是曲面$$S$$在任意一点的切方向的函数，它与法曲率有密切的关系，实际上测地挠率是法曲率作为切方向的函数的导数之半。

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
\kappa_g \boldsymbol{e}_2 = \bigg( \frac{\mathrm{d}^2 u^\gamma}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^\gamma \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg) \boldsymbol{r}_\gamma
$$

显然$$\boldsymbol{r}_1$$和$$\boldsymbol{r}_2$$是线性无关的，因此$$\kappa_g \equiv 0$$的充分必要条件是

$$
\frac{\mathrm{d}^2 u^\gamma}{\mathrm{d} s^2} + \Gamma_{\alpha \beta}^\gamma \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} = 0
$$

这就是曲面$$S$$上的**测地线所满足的微分方程**，并且该方程只涉及曲面$$S$$的第一基本形式，而与曲面$$S$$的第二基本形式无关。因此，这是曲面$$S$$上的测地线属于曲面内蕴几何范畴的微分方程。

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
\frac{\mathrm{d} f (s)}{\mathrm{d} s} &= \frac{\partial g_{\alpha \beta}}{\partial u^\gamma} \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} + 2 g_{\alpha \beta} \frac{\mathrm{d}^2 u^\alpha}{\mathrm{d} s^2} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \\
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
g_{\alpha \beta} (u_0^1, u_0^2) v_0^\alpha v_0^\beta = 1
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

则称$$u^\alpha (s, t)$$是曲线$$C$$的一个**变分**。如果进一步有

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
L(C_t) = \int_a^b \sqrt{g_{\alpha \beta} (u^1 (s, t), u^2 (s, t)) \frac{\partial u^\alpha (s, t)}{\partial s} \frac{\partial u^\beta (s, t)}{\partial s}} \ \mathrm{d} s
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
  g_{\alpha \beta} \frac{\mathrm{d}^2 u^\beta}{\mathrm{d} s^2} \\
  &+ \frac{1}{2} \bigg( 
  \frac{\partial g_{\alpha \beta}}{\partial u^\gamma} + \frac{\partial g_{\alpha \gamma}}{\partial u^\beta} - \frac{\partial g_{\gamma \beta}}{\partial u^\alpha}
  \bigg)
  \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\beta}{\mathrm{d} s} 
\bigg) \bigg] \ \mathrm{d} s \\
&= g_{\alpha \beta} v^\alpha \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg\vert_{s = a}^{s = b} - \int_a^b g_{\alpha \beta} v^\alpha \bigg( \frac{\mathrm{d}^2 u^\beta}{\mathrm{d} s^2} +\Gamma_{\gamma \delta}^\beta \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\delta}{\mathrm{d} s} \bigg) \ \mathrm{d} s
\end{aligned}
$$

假定变分有固定的端点，则$$v^\alpha (a) = v^\alpha (b) = 0$$，于是

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

在空间中选择适当的坐标系始终是几何学中的重要课题。对于只有第一基本形式的曲面而言，这种适当的坐标系应该是能够把曲面的第一基本形式最简单地表示出来的参数系。本节要构造这种特殊的参数系，统称为测地坐标系。

### 测地线族

首先叙述在曲面上覆盖了一个区域的测地线族的概念。假定在曲面$$S$$上有依赖一个参数的测地线族$$\Sigma$$，如果对于区域$$D \subset S$$上的每一个点$$p$$，有且只有一条属于$$\Sigma$$的测地线经过点$$p$$，则称$$\Sigma$$是在曲面$$S$$上覆盖了区域$$D$$的一个测地线族。很明显，如果把$$\Sigma$$中的测地线都限制在区域$$D$$上，则覆盖了区域$$D$$的测地线族$$\Sigma$$中的任意两条不同的测地线都不会彼此相交。

如果$$\Sigma$$是曲面$$S$$上覆盖了区域$$D$$的一个测地线族，则在$$D$$内有另一个曲线族记为$$\Sigma_1$$，它是由$$\Sigma$$的正交轨线构成的。于是区域$$D$$内的任意一点$$p$$必有一个邻域$$U \subset D$$和参数系$$(u, v)$$，使得$$\Sigma$$和$$\Sigma_1$$中的曲线在$$U$$上的限制分别是曲面的$$u$$-曲线族和$$v$$-曲线族。实际上，测地线族$$\Sigma$$中的每一条测地线的切向量构成区域$$D$$上的一个处处非零的切向量场$$\boldsymbol{a}$$, 同时它也在区域$$D$$上决定了与之正交的另一个处处非零的切向量场$$\boldsymbol{b}$$，后者与$$\Sigma_1$$中的曲线处处相切。[定理3.2](/2023/10/18/DifferentialGeometry-NOTES-03.html#曲面上正交参数曲线网的存在性)断言：在区域$$D$$内的任意一点$$p$$的一个邻域$$U \subset D$$内必存在参数系$$(u, v)$$，使得$$u$$-曲线和$$v$$-曲线分别和切向量场$$\boldsymbol{a}$$和$$\boldsymbol{b}$$相切，这就是说，$$\Sigma$$是由$$u$$-曲线组成的(至多每一条曲线差一个重新参数化)，而$$\Sigma_1$$是由$$v$$-曲线组成的(至多每一条曲线差一个重新参数化)。由于曲线族$$\Sigma$$和$$\Sigma_1$$是彼此正交的，故曲面$$S$$的第一基本形式可以写成

$$
\mathrm{I} = E (\mathrm{d} u)^2 + G (\mathrm{d} v)^2
$$

由于$$u$$-曲线是测地线，它的测地曲率$$\kappa_{g1}$$为零，根据Liouville公式得到

$$
\kappa_{g1} = -\frac{1}{2 \sqrt{G}} \frac{\partial \log{E}}{\partial v} = 0
$$

即

$$
\frac{\partial E}{\partial v} = 0
$$

这说明$$E(u, v)$$只是$$u$$的函数，与$$v$$无关，因此可以写成$$E(u)$$。作参数变换

$$
\begin{cases}
\begin{aligned}
\tilde{u} &= \int_{u_0}^{u} \sqrt{E(u)} \ \mathrm{d} u \\
\tilde{v} &= v
\end{aligned}
\end{cases}
$$

则曲面$$S$$的第一基本形式在$$U$$上的限制成为

$$
\mathrm{I} = (\mathrm{d} \tilde{u})^2 + \tilde{G} (\tilde{u}, \tilde{v}) (\mathrm{d} \tilde{v})^2
$$

由此可以得到下面的定理：

**定理6.8** 设$$\Sigma$$是曲面$$S$$上覆盖了区域$$D$$的测地曲线族，$$\Sigma_1$$是由在区域$$D$$内与$$\Sigma$$中曲线正交的轨线构成的曲线族，则$$\Sigma_1$$中的任意两条曲线在测地线族$$\Sigma$$中的各条测地线上截出的曲线段的长度都相等。
{:.info}

**证明** 假定在区域$$D$$上取参数系$$(\tilde{u}, \tilde{v})$$，使得曲面$$S$$的第一基本形式在$$D$$上为

$$
\mathrm{I} = (\mathrm{d} \tilde{u})^2 + \tilde{G} (\tilde{u}, \tilde{v}) (\mathrm{d} \tilde{v})^2
$$

在$$\Sigma_1$$中取定两条曲线，设为$$C_1: \tilde{u} = u_1$$，$$C_2: \tilde{u} = u_2$$，假定$$u_1 \lt u_2$$。又设$$C: \tilde{v} = v_0$$是属于测地线族$$\Sigma$$的一条曲线，它被曲线$$C_1$$和$$C_2$$所截，截得的长度是

$$
\int_{u_1}^{u_2} \sqrt{\mathrm{I}} \bigg\vert_{\tilde{v} = v_0} = \int_{u_1}^{u_2} \ \mathrm{d} \tilde{u} = u_2 - u_1
$$

它与$$v_0$$的值无关。证毕∎

**定理6.8**的直观意义是，覆盖区域$$D$$的测地线族的任意两条正交轨线之间的距离是处处相等的。因此从这个意义上说，覆盖区域$$D$$的测地线族的任意两条正交轨线是测地平行的。

**定理6.9** 设$$C$$是曲面$$S$$上连接$$p$$，$$q$$两点的一条测地线。如果曲线$$C$$能够嵌入到一个覆盖了区域$$D$$的测地线族$$\Sigma$$中去，并且$$p, q \in D$$，则曲线$$C$$是在区域$$D$$内连接$$p$$，$$q$$两点的最短线。
{:.info}

**证明** 假定在区域$$D$$上取参数系$$(\tilde{u}, \tilde{v})$$，使得曲面$$S$$的第一基本形式在$$D$$上为

$$
\mathrm{I} = (\mathrm{d} \tilde{u})^2 + \tilde{G} (\tilde{u}, \tilde{v}) (\mathrm{d} \tilde{v})^2
$$

曲线$$C$$对应于$$\tilde{v} = 0$$，$$p$$的曲纹坐标是$$(0, 0)$$，而$$q$$的曲纹坐标是$$(l, 0)$$，其中$$l$$是曲线$$C$$的长度。若$$\tilde{C}$$是区域$$D$$内连接$$p$$，$$q$$两点的任意一条曲线，设它的参数方程是$$\tilde{u} = u(t)$$，$$\tilde{v} = v(t)$$，$$0 \leq t \leq l$$，并且$$u(0) = 0$$，$$u(l) = l$$，$$v(0) = v(l) = 0$$，则它的长度是

$$
\begin{aligned}
L(\tilde{C}) &= \int_0^l \sqrt{\bigg( \frac{\mathrm{d} u(t)}{\mathrm{d} t} \bigg)^2 + \tilde{G}(u(t), v(t)) \bigg( \frac{\mathrm{d} v(t)}{\mathrm{d} t} \bigg)^2} \ \mathrm{d} s \\
&\geq \int_0^l \bigg\vert \frac{\mathrm{d} u(t)}{\mathrm{d} t} \bigg\vert  \ \mathrm{d} s \geq \int_0^l \mathrm{d} u(t) = l
\end{aligned}
$$

因此$$L(\tilde{C}) \geq L(C)$$。证毕∎

在曲面$$S$$上构造覆盖某个区域的测地线族的方法有很多。在本节，我们介绍两种方法，它们所对应的参数系分别称为测地平行坐标系和测地极坐标系。

### 测地平行坐标系

首先在曲面$$S$$上取定一条测地线$$C$$，然后经过曲线$$C$$上每一点作一条测地线与曲线$$C$$正交，将这些测地线构成的曲线族记为$$\Sigma$$，则曲线族$$\Sigma$$必定覆盖了曲线$$C$$的一个邻域$$U$$。

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/RgFNhTW.png" width="80%">
</div>

根据前面的讨论得知，在曲线$$C$$的邻域$$U$$内存在参数系$$(u, v)$$，使得$$\Sigma$$恰好是$$u$$-曲线族，而曲线$$C$$对应于曲线$$u = 0$$，并且曲面$$S$$的第一基本形式成为

$$
\mathrm{I} = (\mathrm{d} u)^2 + G(u, v) (\mathrm{d} v)^2
$$

在必要时经过适当的参数变换，例如$$\tilde{v} = \int_{v_0}^v \sqrt{G(0, v)} \ \mathrm{d}v$$，总可以假定在$$u = 0$$时参数$$v$$是曲线$$C$$的弧长参数，因此

$$
G(0, v) = 1
$$

又因为曲线$$C: u = 0$$本身是测地线，它的测地曲率

$$
\kappa_{g2} \vert_{u = 0} = \frac{1}{2} \frac{\partial \log{G}}{\partial u} \bigg\vert_{u = 0} = 0
$$

因此

$$
G_u (0, v) = 0
$$

这样，我们有

**定理6.10** 在曲面$$S$$的每一点$$p$$的一个充分小的邻域$$U$$内必定存在参数系$$(u, v)$$，使得点$$p$$对应于$$u = 0$$，$$v = 0$$，而曲面$$S$$的第一基本形式成为$$\mathrm{I} = (\mathrm{d} u)^2 + G(u, v) (\mathrm{d} v)^2$$，其中$$G(u, v)$$满足条件$$G(0, v) = 1$$，$$\frac{\partial G (u, v)}{\partial u} (0, v) = 0$$。这样的参数系$$(u, v)$$称为曲面$$S$$在点$$p$$附近的**测地平行坐标系**。
{:.info}

很明显，平面上的测地平行坐标系就是通常的笛卡儿直角坐标系。

### 法坐标系

现在我们采取另一种做法，先引进曲面$$S$$在点$$p$$的法坐标系，采用张量记号。在曲面$$S$$上取定一点$$p$$，假定$$(u^1, u^2)$$是曲面$$S$$在点$$p$$附近的正交参数系，$$u^1 (p) = 0$$，$$u^2 (p) = 0$$，于是曲面$$S$$的第一基本形式成为

$$
\mathrm{I} = g_{11} (\mathrm{d} u^1)^2 + g_{22} (\mathrm{d} u^2)^2, \ \ \ g_{12} = g_{21} = 0
$$

并且可以假定

$$
g_{11} (0, 0) = 1, \ \ \ g_{22} (0, 0) = 1
$$

这样，$$\{ p; \boldsymbol{r}_1\vert_p, \boldsymbol{r}_2\vert_p \}$$是曲面$$S$$在点$$p$$的切空间$$T_p S$$上的一个单位正交标架。首先，我们要定义映射$$\exp_p: T_p S \rightarrow S$$，称为曲面$$S$$在点$$p$$的指数映射。

根据**定理6.6**，对于在点$$p$$的任意一个切向量$$\boldsymbol{v}$$，存在唯一的一条测地线经过点$$p$$，并且以$$\boldsymbol{v}$$为它在点$$p$$的切向量，记为$$\gamma (s) = \gamma (s; \boldsymbol{v})$$。于是

$$
\gamma (0) = p, \ \ \ \gamma' (0) = \boldsymbol{v}
$$

并且由上式得知

$$
\vert \gamma' (s) \vert = \vert \gamma' (0) \vert = \vert \boldsymbol{v} \vert \text{(常数)}
$$

记$$u^\alpha (s) = u^\alpha (\gamma (s))$$，这是测地线$$\gamma (s)$$的参数方程，并且参数$$s$$与弧长成比例。让$$s$$作变量替换$$s = \lambda t$$，其中$$\lambda \gt 0$$是常数，并且命

$$
\tilde{\gamma} (t) = \gamma (\lambda t) = \gamma (\lambda t; \boldsymbol{v})
$$

它的参数方程是

$$
\tilde{u}^\alpha (t) = u^\alpha (\tilde{\gamma} (t)) = u^\alpha (\gamma (\lambda t)) = u^\alpha (\lambda t)
$$

那么

$$
\frac{\mathrm{d} \tilde{u}^\alpha (t)}{\mathrm{d} t} = \lambda \frac{\mathrm{d} u^\alpha (s)}{\mathrm{d} s}
$$

$$
\frac{\mathrm{d}^2 \tilde{u}^\alpha (t)}{\mathrm{d} t^2} = \lambda^2 \frac{\mathrm{d}^2 u^\alpha (s)}{\mathrm{d} s^2}
$$

因此

$$
\frac{\mathrm{d}^2 \tilde{u}^\alpha (t)}{\mathrm{d} t^2} + \Gamma_{\beta \gamma}^\alpha \frac{\mathrm{d} \tilde{u}^\beta (t)}{\mathrm{d} t} \frac{\mathrm{d} \tilde{u}^\gamma (t)}{\mathrm{d} t} \\
= \lambda^2 \bigg( \frac{\mathrm{d}^2 u^\alpha (s)}{\mathrm{d} s^2} + \Gamma_{\beta \gamma}^\alpha \frac{\mathrm{d} u^\beta (s)}{\mathrm{d} s} \frac{\mathrm{d} u^\gamma (s)}{\mathrm{d} s} \bigg) = 0
$$

这说明$$\tilde{\gamma} (t)$$仍然是一条测地线，并且

$$
\tilde{\gamma} (0) = \gamma (0) = p, \ \ \ \tilde{\gamma}' (0) = \lambda \gamma' (0) = \lambda \boldsymbol{v}
$$

由此可见，$$\tilde{\gamma} (t)$$是一条从点$$p$$出发、以$$\lambda \boldsymbol{v}$$为它在点$$p$$为切向量的测地线。根据**定理6.6**的唯一性以及记号$$\gamma (s; \boldsymbol{v})$$的意义得知，必定有

$$
\tilde{\gamma} (t) = \gamma (\lambda t; \boldsymbol{v}) = \gamma (t; \lambda \boldsymbol{v})
$$

上式的意义是：对于给定的切向量$$\boldsymbol{v}$$来说，测地线$$\gamma(s; \boldsymbol{v})$$定义域可能是某个充分小的区间$$(-\varepsilon, \varepsilon)$$。如果将初始切向量$$\boldsymbol{v}$$的长度成倍地缩小，则测地线$$\gamma (s; \boldsymbol{v})$$的定义域将会成倍地增大。这就是说，当切向量$$\boldsymbol{v}$$的长度充分小时，可以使测地线$$\gamma (s; \boldsymbol{v})$$的定义域足够大。因此，在切空间$$T_p S$$上可以取原点的一个充分小的邻域$$U$$，使得由

$$
\exp_p (\boldsymbol{v}) = \gamma (1; \boldsymbol{v}), \ \ \ \forall \boldsymbol{v} \in U
$$

给出的映射$$\exp_p: U \rightarrow S$$有定义。该映射$$\exp_p: U \rightarrow S$$称为曲面$$S$$在点$$p$$的**指数映射**，它的几何意义是明显的。当$$\boldsymbol{v} = \boldsymbol{0}$$时，$$\exp_p (\boldsymbol{0}) = p$$；当$$\boldsymbol{v} \neq \boldsymbol{0}$$时，命$$\boldsymbol{v}_0 = \frac{\boldsymbol{v}}{\vert \boldsymbol{v} \vert}$$，则$$\boldsymbol{v}_0$$是$$\boldsymbol{v}$$的单位方向向量。根据关系式$$\gamma (\lambda t; \boldsymbol{v}) = \gamma (t; \lambda \boldsymbol{v})$$有

$$
\gamma (1; \boldsymbol{v}) = \gamma (1; \vert \boldsymbol{v} \vert \boldsymbol{v}_0) = \gamma (\vert \boldsymbol{v} \vert; \boldsymbol{v}_0)
$$

由此可见，若以单位切向量$$\boldsymbol{v}_0$$为初始切向量作经过点$$p$$的测地线$$\gamma (s; \boldsymbol{v}_0)$$，其中$$s$$是弧长参数，则在该测地线上截取$$s = \vert \boldsymbol{v} \vert$$的点正好是指数映射$$\exp_p$$下的像$$\exp_p (\boldsymbol{v}) = \gamma (1; \boldsymbol{v})$$。根据常微分方程组的解关于初始值的连续可微依赖性得知，指数映射$$\exp_p: U \rightarrow S$$是连续可微的。

假定切空间$$T_p S$$在单位正交标架$$\{ p; \boldsymbol{r}_1\vert_p, \boldsymbol{r}_2\vert_p \}$$下的坐标是$$(v^1, v^2)$$，即在点$$p$$的任意一个切向量$$\boldsymbol{v} \in T_p S$$可以表示为

$$
\boldsymbol{v} = v^1 \boldsymbol{r}_1\vert_p + v^2 \boldsymbol{r}_2\vert_p
$$

我们要说明，切空间$$T_p S$$上的坐标系$$(v^1, v^2)$$经过指数映射$$\exp_p: U \rightarrow S$$成为曲面$$S$$在点$$p$$附近的参数系，这样得到的参数系称为曲面$$S$$在点$$p$$的**法坐标系**。实际上，命

$$
u^\alpha = u^\alpha (\exp_p (\boldsymbol{v})) = u^\alpha (\gamma (1; \boldsymbol{v})) \equiv u^\alpha (v^1, v^2), \ \ \ \alpha = 1, 2
$$

它们是参数$$v^1$$，$$v^2$$的连续可微函数。任意取定$$\boldsymbol{v} \in U$$，命

$$
u^\alpha (t) = u^\alpha (\exp_p (t \boldsymbol{v})) = u^\alpha (\gamma (1; t \boldsymbol{v}))
$$

因此

$$
u^\alpha (t) = u^\alpha (t v^1, t v^2)
$$

这正好是曲面$$S$$上经过点$$p$$、以$$\boldsymbol{v}$$为初始切向量的测地线$$\gamma (t; \boldsymbol{v})$$的参数方程。因此

$$
u^\alpha (0) = u^\alpha (0, 0) = 0, \ \ \ \alpha = 1, 2
$$

并且

$$
\boldsymbol{v} = \gamma' (t; \boldsymbol{v}) \vert_{t = 0} = \frac{\mathrm{d} u^\alpha (t)}{\mathrm{d} t} \bigg\vert_{t=0} \boldsymbol{r}_\alpha \vert_p = \frac{\partial u^\alpha}{\partial v^\beta} \bigg\vert_p \cdot v^\beta \boldsymbol{r}_\alpha \vert_p
$$

将上式与$$\boldsymbol{v} = v^1 \boldsymbol{r}_1\vert_p + v^2 \boldsymbol{r}_2\vert_p$$相比较得到

$$
\frac{\partial u^\alpha}{\partial v^\beta} \bigg\vert_p = \delta_\beta^\alpha = 
\begin{cases}
1, \ \ \ \alpha = \beta \\
0, \ \ \ \alpha \neq \beta \\
\end{cases}
$$

由此可见，变换$$u^\alpha = u^\alpha (v^1, v^2)$$是曲面$$S$$在点$$p$$附近的正则参数变换，因此$$(v^1, v^2)$$是曲面$$S$$在点$$p$$附近容许的参数系。

曲面$$S$$在点$$p$$的法坐标系$$(v^1, v^2)$$的特征是：经过点$$p$$的测地线$$\gamma (t; \boldsymbol{v})$$的参数方程

$$
v^\alpha (t) = v^\alpha (\gamma (t; \boldsymbol{v})) = v^\alpha (u^1 (t), u^2 (t))
$$

是$$t$$的线性函数。事实上，设参数变换$$u^\alpha = u^\alpha (v^1, v^2)$$的逆变换是

$$
v^\alpha = v^\alpha (u^1, u^2)
$$

即它们关于任意的$$(u^1, u^2)$$满足恒等式

$$
u^\alpha \equiv u^\alpha (v^1 (u^1, u^2), v^2 (u^1, u^2)), \ \ \ \alpha = 1, 2
$$

特别是将测地线$$\gamma(t; \boldsymbol{v})$$的参数方程$$(u^1 (t), u^2 (t))$$带入上式得到

$$
\begin{aligned}
u^\alpha (t) &= u^\alpha (v^1 (u^1 (t), u^2 (t)), v^2 (u^1 (t), u^2 (t))) \\
&= u^\alpha (v^1 (t), v^2 (t))
\end{aligned}
$$

另一方面

$$
u^\alpha (t) = u^\alpha (t v^1, t v^2)
$$

根据在给定的参数系下点的曲纹坐标的唯一性，比较上面两式，得到经过点$$p$$的测地线$$\gamma(t; \boldsymbol{v})$$的参数方程是

$$
\begin{cases}
\begin{aligned}
v^1 (t) &= t v^1 \\ v^2 (t) &= t v^2
\end{aligned}
\end{cases}
$$

假定曲面$$S$$在点$$p$$的法坐标系$$(v^1, v^2)$$下的第一类基本量是$$\tilde{g}_{\alpha \beta}$$，那么

$$
\tilde{g}_{\alpha \beta} = g_{\gamma \delta} \frac{\partial u^\gamma}{v^\alpha} \frac{\partial u^\delta}{v^\beta}
$$

特别地由$$\frac{\partial u^\alpha}{\partial v^\beta} \bigg\vert_p = \delta_\beta^\alpha$$得知

$$
\tilde{g}_{11} (0, 0) = \tilde{g}_{22} (0, 0) = g_{11} (0, 0) = g_{22} (0, 0) = 1
$$

$$
\tilde{g}_{12} (0, 0) = \tilde{g}_{21} (0, 0) = g_{12} (0, 0) = g_{21} (0, 0) = 0
$$

我们还能够得到关于$$\tilde{g}_{\alpha \beta}$$的更多的信息。由于$$v^\alpha (t) = t v^\alpha$$是曲面$$S$$上经过点$$p$$、以$$\boldsymbol{v}$$为切向量的测地线，它应该满足测地线的微分方程

$$
\frac{\mathrm{d}^2 v^\gamma (t)}{\mathrm{d} t^2} + \tilde{\Gamma}_{\alpha \beta}^\gamma \frac{\mathrm{d} v^\alpha (t)}{\mathrm{d} t} \frac{\mathrm{d} v^\beta (t)}{\mathrm{d} t} = \tilde{\Gamma}_{\alpha \beta}^\gamma (\gamma(t; \boldsymbol{v})) v^\alpha v^\beta = 0
$$

其中$$\tilde{\Gamma}_{\alpha \beta}^\gamma$$是关于$$\tilde{g}_{\alpha \beta}$$的Christoffel记号。取$$t = 0$$，则上式成为

$$
\tilde{\Gamma}_{\alpha \beta}^\gamma (p) v^\alpha v^\beta = 0
$$

在$$U$$上这是关于$$\boldsymbol{v} = (v^1, v^2)$$的恒等式，并且$$\tilde{\Gamma}_{\alpha \beta}^\gamma (p) = \tilde{\Gamma}_{\beta \alpha}^\gamma (p)$$，因此

$$
\tilde{\Gamma}_{\alpha \beta}^\gamma (p) = 0
$$

由此可见，我们有下面的定理：

**定理6.11** 曲面$$S$$在任意一点$$p$$的附近必有法坐标系$$(v^1, v^2)$$，在此坐标系下从点$$p$$出发、以$$(v_0^1, v_0^2)$$为切向量的测地线的参数方程是$$v^1 (t) = t v_0^1$$，$$v^2 (t) = t v_0^2$$，并且曲面$$S$$的第一类基本量$$\tilde{g}_{\alpha \beta}$$满足$$\tilde{g}_{11}(p) = \tilde{g}_{22}(p) = 1$$，$$\tilde{g}_{12}(p) = \tilde{g}_{21}(p) = 0$$，$$\tilde{\Gamma}_{\alpha \beta}^\gamma (p) = 0$$，因此
$$
\frac{\partial \tilde{g}_{\alpha \beta}}{\partial v^\gamma} (p) = \tilde{g}_{\alpha \delta} \tilde{\Gamma}_{\beta \gamma}^\delta (p) + \tilde{g}_{\beta \delta} \tilde{\Gamma}_{\alpha \gamma}^\delta (p) = 0
$$
。
{:.info}

需要指出的是，在点$$p$$的法坐标系$$(v^1, v^2)$$下，曲面$$S$$的第一类基本量$$\tilde{g}_{\alpha \beta}$$在点$$p$$有很好的性质，但在点$$p$$意外却未必有下列等式：

$$
\tilde{g}_{12} = \tilde{g}_{21} = 0
$$

即法坐标系在点$$p$$以外未必是正交参数系。

### 测地极坐标系

最后，我们来看曲面$$S$$在点$$p$$的测地极坐标系$$(s, \theta)$$。设$$(v^1, v^2)$$是切空间$$T_p S$$中的笛卡尔直角坐标系，则在切空间$$T_p S$$上可以取极坐标系$$(s, \theta)$$，使得

$$
\begin{cases}
\begin{aligned}
v^1 &= s \cos{\theta} \\
v^2 &= s \sin{\theta} \\
\end{aligned}
\end{cases}
$$

这样的坐标系适用于切空间$$T_p S$$中除去从点$$p$$出发的一条射线后余下的区域。于是$$(v^1, v^2)$$通过指数映射$$\exp_p: U \rightarrow S$$成为曲面$$S$$在点$$p$$附近的法坐标系，同时$$(s, \theta)$$成为曲面$$S$$在点$$p$$附近、除去从点$$p$$出发的一条测地线后余下的区域上的一个新的参数系，称为曲面$$S$$在点$$p$$的**测地极坐标系**。从测地极坐标系$$(s, \theta)$$到法坐标系$$(v^1, v^2)$$的坐标变换恰好是由上式给出的。

为确定起见，假定所去掉的射线对应于$$\theta = \pi$$，于是在切空间$$T_p S$$上测地极坐标系$$(s, \theta)$$的适用范围是$$0 \lt s \lt \infty$$，$$-\pi \lt \theta \lt \pi$$。用$$U_0$$表示区域$$U$$是在去掉从点$$p$$出发的这条对应的测地线后余下的区域。对于任意固定的$$-\pi \lt \theta_0 \lt \pi$$，让$$s$$变化，则上面方程组给出$$T_p S$$中从原点出发的一条射线，而在曲面$$S$$上得到从点$$p$$出发的一条测地线，该测地线用法坐标系表示的参数方程是

$$
\begin{cases}
\begin{aligned}
v^1 (s) &= s \cos{\theta_0} \\
v^2 (s) &= s \sin{\theta_0} \\
\end{aligned}
\end{cases}
$$

将所有这样的测地线的集合记为$$\Sigma$$，那么$$\Sigma$$是覆盖了区域$$U_0$$的测地线族。任意固定一个充分小的值$$s = s_0 \gt 0$$，让$$\theta$$变化，则在曲面$$S$$上得到一条曲线，它是在测地线族$$\Sigma$$中每一条测地线上从点$$p$$出发、截取长度为$$s_0$$的点所得到的轨迹，称为曲面$$S$$上以点$$p$$为中心、以$$s_0$$为半径的**测地圆**。将以点$$p$$为中心的全体测地圆的集合记为$$\Sigma_1$$。

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/3WpCyGW.png" width="80%">
</div>

**引理** 点$$p$$出发的测地线与以点$$p$$为中心的测地圆是彼此正交的，即曲线族$$\Sigma_1$$中的每一条曲线是测地线族$$\Sigma$$的正交轨线。
{:.info}

通常把上面的引理称为**Gauss引理**。

**证明** 假定$$(u^1, u^2)$$是点$$p$$附近的正交参数系，并且点$$p$$对应于坐标$$u^1 = 0$$，$$u^2 = 0$$。设曲面$$S$$的第一基本形式是

$$
\mathrm{I} = g_{\alpha \beta} \mathrm{d} u^\alpha \mathrm{d} u^\beta
$$

用$$\theta$$表示在点$$p$$的切向量与$$u^1$$-曲线的夹角。根据**定理6.6**，经过点$$p$$、与$$u^1$$-曲线的夹角为$$\theta$$的测地线记为$$C_\theta$$，其参数方程是$$u^\alpha = u^\alpha (s, \theta)$$，其中$$s$$是测地线的弧长参数，并且$$u^\alpha (s, \theta)$$是$$s$$，$$\theta$$的连续可微函数。曲线族$$\Sigma$$中的曲线$$\Sigma_\theta$$就是$$\theta$$为常数的曲线，曲线族$$\Sigma_1$$中的曲线就是$$s$$为常数的曲线。设曲线$$C$$是测地线$$\theta = \theta_0$$，$$0 \leq s \leq s_0$$，即它的参数方程是$$u^\alpha = u^\alpha (s, \theta_0)$$，$$0 \leq s \leq s_0$$，那么曲线族$$\Sigma$$是它的一个变分，其变分向量场由

$$
w^\alpha (s) = \frac{\partial u^\alpha (s, \theta)}{\partial \theta} \bigg\vert_{\theta = \theta_0}
$$

给出。由于变分曲线都是从点$$p$$出发的，故$$u^\alpha (0, \theta) = 0$$，所以$$w^\alpha (0) = 0$$，$$\alpha = 1, 2$$。然而$$w^\alpha (s_0) \boldsymbol{r}_\alpha$$是测地圆$$u^\alpha = u^\alpha (s_0, \theta)$$在$$\theta = \theta_0$$处的切向量，根据曲线弧长的第一变分公式得到

$$
\begin{aligned}
\frac{\mathrm{d}}{\mathrm{d} \theta} \bigg\vert_{\theta = \theta_0} L(C_\theta) &= g_{\alpha \beta} w^\alpha (s) \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg\vert_{s=0}^{s=s_0} - \int_0^r g_{\alpha \beta} w^\alpha \bigg( \frac{\mathrm{d}^2 u^\beta}{\mathrm{d} s^2} + \Gamma_{\gamma \delta}^\beta \frac{\mathrm{d} u^\gamma}{\mathrm{d} s} \frac{\mathrm{d} u^\delta}{\mathrm{d} s} \bigg) \mathrm{d} s \\
&= g_{\alpha \beta} w^\alpha (s_0) \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg\vert_{s=0}
\end{aligned}
$$

但是，每一条测地线$$C_\theta: u^\alpha = u^\alpha (s, \theta)$$，$$0 \leq s \leq s_0$$的长度都是$$s_0$$，即$$L(C_\theta) = s_0$$，因此上式的最左段为零，于是

$$
g_{\alpha \beta} w^\alpha (s_0) \frac{\mathrm{d} u^\beta}{\mathrm{d} s} \bigg\vert_{s=0} = 0
$$

这意味着，测地线$$C$$与直径为$$s_0$$的测地圆是彼此正交的。证毕∎

由于$$\Sigma_1$$是测地线族$$\Sigma$$的正交轨道族，$$s$$是曲线族$$\Sigma$$中测地线的弧长参数，于是$$(s, \theta)$$是$$U_0$$上的参数系，而且曲面$$S$$的第一基本形式成为

$$
\mathrm{I} = (\mathrm{d} s)^2 + G(s, \theta) (\mathrm{d} \theta)^2
$$

我们想要知道函数$$G(s, \theta)$$的更多性质。已知曲面$$S$$在点$$p$$的法坐标系$$(v^1, v^2)$$和测地极坐标系$$(s, \theta)$$的坐标变换是由

$$
\begin{cases}
\begin{aligned}
v^1 &= s \cos{\theta} \\
v^2 &= s \sin{\theta} \\
\end{aligned}
\end{cases}
$$

给出的，因此

$$
\begin{cases}
\begin{aligned}
&(v^1)^2 + (v^2)^2 = s^2 \\
&\frac{v^2}{v^1} = \tan{\theta}
\end{aligned}
\end{cases}
$$

同时

$$
\begin{cases}
\begin{aligned}
\mathrm{d} v^1 &= \cos{\theta} \mathrm{d} s - s \sin{\theta} \mathrm{d} \theta \\
\mathrm{d} v^2 &= \sin{\theta} \mathrm{d} s + s \cos{\theta} \mathrm{d} \theta
\end{aligned}
\end{cases}
$$

所以

$$
\begin{cases}
\begin{aligned}
\mathrm{d} s &= \frac{v^1 \mathrm{d} v^1 + v^2 \mathrm{d} v^2}{s} \\
\mathrm{d} \theta &= \frac{v^1 \mathrm{d} v^2 - v^2 \mathrm{d} v^1}{s^2}
\end{aligned}
\end{cases}
$$

将上式代入第一基本形式得到

$$
\begin{aligned}
\mathrm{I} &= (\mathrm{d} s)^2 + G(s, \theta) (\mathrm{d} \theta)^2 \\
&= \bigg( \frac{v^1}{s} \mathrm{d} v^1 + \frac{v^2}{s} \mathrm{d} v^2 \bigg)^2 + G(s, \theta) \bigg( \frac{v^1}{s^2} \mathrm{d} v^2 + \frac{v^2}{s^2} \mathrm{d} v^1 \bigg)^2 \\
&= \bigg( \frac{(v^1)^2}{s^2} + G\frac{(v^2)^2}{s^4} \bigg) (\mathrm{d} v^1)^2 + \frac{2 v^1 v^2}{s^2} \bigg( 1 - \frac{G}{s^2} \bigg) \mathrm{d} v^1 \mathrm{d} v^2 + \bigg( \frac{(v^2)^2}{s^2} + G\frac{(v^1)^2}{s^4} \bigg) (\mathrm{d} v^2)^2 \\
&= \bigg( 1 + \frac{(v^2)^2}{s^2} \bigg( \frac{G}{s^2} - 1 \bigg) \bigg) (\mathrm{d} v^1)^2 + \frac{2 v^1 v^2}{s^2} \bigg( 1 - \frac{G}{s^2} \bigg) \mathrm{d} v^1 \mathrm{d} v^2 + \bigg( 1 + \frac{(v^1)^2}{s^2} \bigg( \frac{G}{s^2} - 1 \bigg) \bigg) (\mathrm{d} v^2)^2
\end{aligned}
$$

由此可见

$$
\begin{cases}
\begin{aligned}
\tilde{g}_{11} &= 1 + \frac{(v^2)^2}{s^2} \bigg( \frac{G}{s^2} - 1 \bigg) = 1 + \sin^2{\theta} \bigg( \frac{G}{s^2} - 1 \bigg) \\
\tilde{g}_{12} &= \frac{v^1 v^2}{s^2} \bigg( 1 - \frac{G}{s^2} \bigg) = \sin{\theta} \cos{\theta} \bigg( 1 - \frac{G}{s^2} \bigg) \\
\tilde{g}_{22} &= 1 + \frac{(v^1)^2}{s^2} \bigg( \frac{G}{s^2} - 1 \bigg) = 1 + \cos^2{\theta} \bigg( \frac{G}{s^2} - 1 \bigg) \\
\end{aligned}
\end{cases}
$$

与法坐标系下的第一基本量相对比得到

$$
\lim_{s \rightarrow 0} \frac{G (s, \theta)}{s^2} = 1
$$

即

$$
G (s, \theta) = s^2 + o(s^2)
$$

$$
\sqrt{G (s, \theta)} = s + o(s)
$$

因此

$$
\lim_{s \rightarrow 0} \sqrt{G (s, \theta)} = 0
$$

并且

因此

$$
\lim_{s \rightarrow 0} (\sqrt{G (s, \theta)})_s = 1
$$

综合上面的讨论我们有下述定理。

**定理6.12** 在曲面$$S$$的每一点$$p$$的邻域内，除去从点$$p$$出发的一条测地线外，必存在测地极坐标系$$(s, 0)$$，使得曲面$$S$$的第一基本形式成为
$$
\mathrm{I} = (\mathrm{d} s)^2 + G(s, \theta) (\mathrm{d} \theta)^2
$$
其中函数$$G(s, \theta)$$满足条件
$$
\lim_{s \rightarrow 0} \sqrt{G(s, \theta)} = 0
$$
，
$$
\lim_{s \rightarrow 0} \frac{\partial}{\partial s} \sqrt{G(s, \theta)} = 1
$$
。
{:.info}

显然，平面上的极坐标系就是测地极坐标系。

在本节，我们分别介绍了曲面上的测地平行坐标系、法坐标系和测地极坐标系。曲面的第一基本形式在测地平行坐标系和测地极坐标系有最简单的表达式，这就是本节所叙述的**定理6.10**和**定理6.12**。曲面上的法坐标系是将曲面在一点处的切空间的笛卡儿直角坐标系经过指数映射产生的，它的特点是经过该点的测地线参数方程变得十分简单，恰好是参数的线性函数，因而相应的第一类基本量在该点有很好的性质。在维数≥3的黎曼几何情形，测地平行坐标系和测地极坐标系不再以如此简单的形式出现了，但是仍然有法坐标系的理论，其中Gauss引理将是十分重要的基本事实。

## 常曲率曲面

Gauss曲率为常数的曲面称为**常曲率曲面**。在[Gauss曲率为常数的曲面](/2023/11/10/DifferentialGeometry-NOTES-04.html#gauss曲率为常数的曲面)一节我们已经根据常曲率旋转曲面所满足的微分方程算出它的参数方程。在本节，我们将利用测地坐标系决定常曲率曲面的第一基本形式。由此可见，有相同常Gauss曲率的常曲率曲面在局部上是彼此等距的。

假定曲面$$S$$的Gauss曲率$$K$$是常数。在曲面$$S$$上取测地平行坐标系$$(u, v)$$，因而它的第一基本形式为

$$
\mathrm{I} = (\mathrm{d} u)^2 + G(u, v) (\mathrm{d} v)^2
$$

其中$$G(u, v)$$满足条件

$$
G(0, v) = 1, \ \ \ \frac{\partial G}{\partial u} (0, v) = 0
$$

根据Gauss曲率$$K$$的[内蕴表达式](/2023/12/27/DifferentialGeometry-NOTES-05.html#gauss定理)，我们有

$$
K = -\frac{1}{\sqrt{EG}} \bigg[ \bigg( \frac{\big( \sqrt{E} \big)_v}{\sqrt{G}} \bigg)_v + \bigg( \frac{\big( \sqrt{G} \big)_u}{\sqrt{E}} \bigg)_u \bigg] = -\frac{1}{\sqrt{G}} (\sqrt{G})_{uu}
$$

所以$$\sqrt{G}$$作为$$u$$的函数满足常系数二阶线性齐次方程

$$
(\sqrt{G})_{uu} + K \sqrt{G} = 0
$$

初始条件是

$$
G(0, v) = 1, \ \ \ (\sqrt{G})_u (0, v) = 0
$$

齐次方程的特征方程是

$$
\lambda^2 + K = 0
$$

因此，根据$$K$$的不同符号，方程的通解分别为

$$
\sqrt{G} = 
\begin{cases}
\begin{aligned}
&a(v) \cos{(\sqrt{K} u)} + b(v) \sin{(\sqrt{K} u)}, \ \ \ & K \gt 0 \\
&a(v) + b(v) u, \ \ \ & K = 0 \\
&a(v) \cosh{(\sqrt{-K} u)} + b(v) \sinh{(\sqrt{-K} u)}, \ \ \ & K \lt 0 \\
\end{aligned}
\end{cases}
$$

在初始条件下，进一步得到$$\sqrt{G}$$的微分方程的解为

$$
\sqrt{G} = 
\begin{cases}
\begin{aligned}
&\cos{(\sqrt{K} u)}, \ \ \ & K \gt 0 \\
&1, \ \ \ & K = 0 \\
&\cosh{(\sqrt{-K} u)}, \ \ \ & K \lt 0 \\
\end{aligned}
\end{cases}
$$

因此，Gauss曲率为$$K$$的常曲率曲面$$S$$的第一基本形式在测地平行坐标系$$(u, v)$$下有完全确定的表达式，根据其Gauss曲率$$K$$的符号的不同分别为

$$
\mathrm{I} = 
\begin{cases}
\begin{aligned}
&(\mathrm{d} u)^2 + \cos^2{(\sqrt{K} u)} (\mathrm{d} v)^2, \ \ \ & K \gt 0 \\
&(\mathrm{d} u)^2 + (\mathrm{d} v)^2, \ \ \ & K = 0 \\
&(\mathrm{d} u)^2 + \cosh^2{(\sqrt{-K} u)} (\mathrm{d} v)^2, \ \ \ & K \lt 0 \\
\end{aligned}
\end{cases}
$$

由此得到下面的定理：

**定理6.13** 有相同常数Gauss曲率$$K$$的任意两块常曲率曲面在局部上必定可以建立保长对应。
{:.info}

通过前面各节的讨论可以看出，Gauss的绝妙定理启发我们去研究只具有第一基本形式的一张抽象曲面，而不是放在欧氏空间$$\mathbb{R}^3$$中的一张具体的曲面。换句话说，我们所考虑的曲面是两个变数$$u$$，$$v$$的区域$$D$$，并且在$$D$$上指定了一个正定的二次微分形式

$$
(\mathrm{d} s)^2 = E(u, v) (\mathrm{d} u)^2 + 2 F(u, v) \mathrm{d} u \mathrm{d} v + G(u, v) (\mathrm{d} v)^2
$$

称为该抽象曲面上的度量形式。它的几何意义是，抽象曲面在点$$(u, v)$$的切向量$$(\mathrm{d} u, \mathrm{d} v)$$的长度的平方。抽象曲面在一点$$(u, v)$$的两个切向量$$(\mathrm{d} u, \mathrm{d} v)$$和$$(\delta u, \delta v)$$的夹角$$\theta$$余弦是

$$
\cos{\theta} = \frac{E(u, v) \mathrm{d} u \delta u + F(u, v) (\mathrm{d} u \delta v + \delta u \mathrm{d} v) + G(u, v) \mathrm{d} v \delta v}{\sqrt{E (\mathrm{d} u)^2 + 2F \mathrm{d} u \mathrm{d} v + G (\mathrm{d} v)^2} \sqrt{E (\delta u)^2 + 2F \delta u \delta v + G (\delta v)^2}}
$$

曲面上的曲线$$u = u(t)$$，$$v = v(t)$$，$$a \leq t \leq b$$的长度是

$$
\int_a^b \sqrt{E \bigg( \frac{\mathrm{d} u}{\mathrm{d} t} \bigg)^2 + 2F \frac{\mathrm{d} u}{\mathrm{d} t} \frac{\mathrm{d} v}{\mathrm{d} t} + G \bigg( \frac{\mathrm{d} v}{\mathrm{d} t} \bigg)^2 } \ \mathrm{d} t
$$

在1854年，Riemann把Gauss内蕴微分几何的思想一举推广到任意维数$$n$$的情形，开创了现在所称的Riemann几何学。于是，Gauss内蕴微分几何学就是二维的Riemann几何学。在这样的抽象曲面上除了计算上面所述的几何量以外，最主要的几何量是Gauss曲率$$K$$, 以及曲面上的曲线的测地曲率和曲面上的测地线等等由此可见，在抽象曲面上仍然有丰富的几何学可供研究。

最简单的一类抽象曲面就是常曲率曲面，它的第一基本形式是由它的常数Gauss曲率$$K$$完全确定的。非欧几何学的出现是人类思想史的划时代进展。从现代数学的观点来看，从欧氏几何学到非欧几何学的发展实际上就是把平面几何学推广到常曲率曲面上的几何学，更进一步可以推广到一般的Riemann几何学。欧氏几何学和非欧几何学的本质差别在于空间的弯曲程度不同。欧氏空间是平坦的空间，其Gauss曲率$$K$$为零。非欧空间是常弯曲的空间，其Gauss曲率$$K$$是非零常数。空间的弯曲性质的不同决定了该空间中的直线(即测地线)的性状的不同，从而决定了该空间中的(测地)三角形的内角和的不同。在[后面](/2024/04/15/DifferentialGeometry-NOTES-06.html#gauss-bonnet公式)要介绍的Gauss-Bonnet定理将会清晰地揭示这个事实。在本节，我们将进一步讨论常曲率曲面上测地线的性状。

直接计算表明，度量形式

$$
(\mathrm{d} s)^2 = \frac{(\mathrm{d} u)^2 + (\mathrm{d} v)^2}{\bigg(1 + \frac{K}{4} (u^2 + v^2) \bigg)^2}
$$

的Gauss曲率为常数$$K$$。这个公式把常曲率曲面的度量形式写成统一的表达式，这是Riemann首先给出来的。当$$K \geq 0$$时，该抽象曲面的定义域是整个$$uv$$平面；当$$K \lt 0$$时，该抽象曲面的定义域是$$uv$$平面上的一个区域

$$
D = \bigg\{ (u, v): u^2 + v^2 \lt - \frac{4}{K} \bigg\}
$$

设$$K = 0$$，则$$(\mathrm{d} s)^2 = (\mathrm{d} u)^2 + (\mathrm{d} v)^2$$，所以这个抽象曲面就是普通的平面，它上面的测地线就是普通的直线。

设$$K \gt 0$$，则相应的抽象曲面可以看作为，三维欧氏空间$$\mathbb{E}^3$$中半径为$$\frac{1}{\sqrt{K}}$$的球面通过从南极向球面北极处的切平面作球极投影所得的像。具体地说，该投影的表达式是

$$
u = \frac{2x}{\sqrt{K} z + 1}, \ \ \ 
v = \frac{2y}{\sqrt{K} z + 1}, \ \ \ 
x^2 + y^2 + z^2 = \frac{1}{K}
$$

或者反过来得到

$$
\begin{aligned}
x &= \frac{4u}{4 + K(u^2 + v^2)} \\
y &= \frac{4v}{4 + K(u^2 + v^2)} \\
z &= \frac{1}{\sqrt{K}} \frac{4 - K(u^2 + v^2)}{4 + K(u^2 + v^2)} \\
\end{aligned}
$$

直接计算表明，上面定义的球面的第一基本形式恰好是

$$
(\mathrm{d} s)^2 = \frac{(\mathrm{d} u)^2 + (\mathrm{d} v)^2}{\bigg(1 + \frac{K}{4} (u^2 + v^2) \bigg)^2}
$$

在球面上，测地线就是大圆周。很明显，这些大圆周在球极投影下的像是在$$uv$$平面上以原点为中心、以$$\frac{2}{\sqrt{K}}$$为半径的圆周$$C$$，以及经过圆周$$C$$的的任意一对对径点的所有圆周和直线。由此可见，在这个抽象曲面上，任意两条"直线"是彼此相交的。

[前面](/2023/11/10/DifferentialGeometry-NOTES-04.html#负gauss曲率曲面)所介绍的伪球面是负常曲率曲面的例子，但是在该曲面上不是所有的测地线都能够无限地延伸的。要给出常数$$K \lt 0$$时，区域为$$D$$、第一基本形式为$$(\mathrm{d} s)^2 = \frac{(\mathrm{d} u)^2 + (\mathrm{d} v)^2}{\bigg(1 + \frac{K}{4} (u^2 + v^2) \bigg)^2}$$的抽象曲面(称为Klein圆)的具体模型，在三维欧式空间$$\mathbb{E}^3$$中是做不到的。我们引进所谓的洛伦兹空间$$L^3$$，其中的点仍然是一组3个有序的实数$$(x, y ,z)$$，但是任意两个向量$$\boldsymbol{a} = (x_1, y_1, z_1)$$和$$\boldsymbol{b} = (x_2, y_2, z_2)$$的内积定义为

$$
\boldsymbol{a} \cdot \boldsymbol{b} = x_1 x_2 + y_1 y_2 - z_1 z_2
$$

考虑$$L^3$$中的曲面

$$
\Sigma = \bigg\{ (x, y, z) \in L^3: x^2 + y^2 - z^2 = \frac{1}{K}, z \gt 0 \bigg\}
$$

它也可以用参数方程来表示，一种表示方式是所谓的球极投影：将曲面$$\Sigma$$上的任意一点$$(x, y, z)$$与点$$(0, 0, -\frac{1}{\sqrt{-K}})$$连成一条直线，该直线与$$L^3$$中的平面$$z = \frac{1}{\sqrt{-K}}$$交于一点，记为$$(u, v, \frac{1}{\sqrt{-K}})$$，称该点为曲面$$\Sigma$$上的点$$(x, y, z)$$在球极投影下的像。经直接计算得到

$$
u = \frac{2x}{\sqrt{-K} z + 1}, \ \ \ v = \frac{2y}{\sqrt{-K} z + 1}
$$

或者反过来得到

$$
\begin{aligned}
x &= \frac{4u}{4 + K(u^2 + v^2)} \\
y &= \frac{4v}{4 + K(u^2 + v^2)} \\
z &= \frac{1}{\sqrt{-K}} \frac{4 - K(u^2 + v^2)}{4 + K(u^2 + v^2)} \\
\end{aligned}
$$

参数$$(u, v)$$的取值范围正好是区域$$D$$，而且曲面$$\Sigma$$和区域$$D$$在上述球极投影下是一一对应的。对上式求微分得到

$$
\begin{aligned}
\mathrm{d} x &= \frac{4(4 + K(-u^2 + v^2)) \mathrm{d} u - 8 K u v \mathrm{d} v}{(4 + K(u^2 + v^2))^2} \\
\mathrm{d} y &= \frac{- 8 K u v \mathrm{d} u + 4(4 + K(u^2 - v^2)) \mathrm{d} v}{(4 + K(u^2 + v^2))^2} \\
\mathrm{d} z &= \frac{16 \sqrt{-K} (u \mathrm{d} u + v \mathrm{d} v)}{(4 + K(u^2 + v^2))^2} \\
\end{aligned}
$$

因此，洛伦兹空间$$L^3$$在曲面$$\Sigma$$上诱导的第一基本形式是

$$
\mathrm{I} = \frac{16 \big( (\mathrm{d} u)^2 + (\mathrm{d} v)^2 \big)}{(4 + K(u^2 + v^2))^2} = \frac{(\mathrm{d} u)^2 + (\mathrm{d} v)^2}{\bigg(1 + \frac{K}{4} (u^2 + v^2) \bigg)^2}
$$

这正好是前面给出的度量形式，即洛伦兹空间$$L^3$$中具有诱导第一基本形式的曲面$$\Sigma$$是抽象曲面Klein圆$$(D, (ds)^2)$$的模型。如果把洛伦兹空间$$L^3$$称为伪欧氏空间，则曲面$$\Sigma$$相当于"伪"球面。实际上，若把洛伦兹空间$$L^3$$中的点$$(x, y,z)$$仍然记成$$\boldsymbol{r}$$，则曲面$$\Sigma$$满足方程

$$
\boldsymbol{r} \cdot \boldsymbol{r} = \frac{1}{K}, \ \ \ z \gt 0
$$

对上式求微分得到

$$
\mathrm{d} \boldsymbol{r} \cdot \boldsymbol{r} = 0
$$

这表明向径$$\boldsymbol{r}$$与曲面$$\Sigma$$在洛伦兹内积意义下正交，即向径$$\boldsymbol{r}$$是曲面$$\Sigma$$的法向量。用空间$$L^3$$经过原点的平面$$\Pi$$与曲面$$\Sigma$$相交，设交线的参数方程是$$\boldsymbol{r} (s)$$，其中$$s$$是曲线的弧长参数，那么

$$
\frac{\mathrm{d} \boldsymbol{r} (s)}{\mathrm{d} s} \cdot \frac{\mathrm{d} \boldsymbol{r} (s)}{\mathrm{d} s} = 1
$$

求导数得到

$$
\frac{\mathrm{d}^2 \boldsymbol{r} (s)}{\mathrm{d} s^2} \cdot \frac{\mathrm{d} \boldsymbol{r} (s)}{\mathrm{d} s} = 0
$$

因此

$$
\frac{\mathrm{d} \boldsymbol{r} (s)}{\mathrm{d} s} \cdot \boldsymbol{r} (s) = 0
$$

这说明在同一个平面$$\Pi$$内的向量$$\frac{\mathrm{d}^2 \boldsymbol{r} (s)}{\mathrm{d} s^2}$$，$$\boldsymbol{r} (s)$$同时与该平面内的非零向量$$\frac{\mathrm{d} \boldsymbol{r} (s)}{\mathrm{d} s}$$正交，于是曲线$$\boldsymbol{r} (s)$$的曲率向量$$\frac{\mathrm{d}^2 \boldsymbol{r} (s)}{\mathrm{d} s^2}$$(它的方向向量是主法向量)与曲面$$\Sigma$$的法向量$$\boldsymbol{r} (s)$$平行，故曲线$$\boldsymbol{r} (s)$$是曲面$$\Sigma$$上的测地线。反过来可以证明，曲面$$\Sigma$$上的测地线就是这样的曲线。在球极投影下，曲面$$\Sigma$$上的测地线成为$$uv$$平面内与区域$$D$$的边界曲线$$u^2 + v^2 = -\frac{K}{4}$$正交的圆弧或直径。很明显，在抽象曲面Klein圆$$(D, (\mathrm{d} s)^2)$$上，经过"直线"外一点可以作无数条"直线"与已知"直线"不相交，这正是非欧几何学的平行公理。

## 曲面上切向量的平行移动

本节我们要叙述曲面的内蕴微分几何的一个重要的概念，即曲面上的切向量场的协变微分和曲面上的切向量沿曲线的平行移动。为了容易理解起见，我们首先在$$\mathbb{E}^3$$中的曲面上来考虑，然后把这些讨论推广到具有第一基本形式的抽象曲面上去。

### 协变微分

设$$S$$是欧式空间$$\mathbb{E}^3$$中的一个曲面，它的参数方程是$$\boldsymbol{r} = \boldsymbol{r} (u^1, u^2)$$。假定$$\boldsymbol{X} (u^1, u^2)$$是定义在曲面$$S$$上的一个切向量场，所以它在曲面的自然切标架场$$\{ \boldsymbol{r}; \boldsymbol{r}_1, \boldsymbol{r}_2 \}$$下可以表示为

$$
\boldsymbol{X} (u^1, u^2) = x^\alpha (u^1, u^2) \boldsymbol{r}_\alpha (u^1, u^2)
$$

如果$$x^\alpha (u^1, u^2)$$是可微函数，则称切向量场$$\boldsymbol{X} (u^1, u^2)$$是可微的。把$$\boldsymbol{X} (u^1, u^2)$$作为空间$$\mathbb{E}^3$$中定义在曲面$$S$$上的向量场，微分$$\mathrm{d} \boldsymbol{X} (u^1, u^2)$$是有意义的。从直观上看，$$\mathrm{d} \boldsymbol{X} (u^1, u^2)$$是向量场$$\boldsymbol{X} (u^1, u^2)$$在无限邻近的两个点$$(u^1, u^2)$$和$$(u^1 + \mathrm{d} u^1, u^2 + \mathrm{d} u^2)$$的值之差：

$$
\mathrm{d} \boldsymbol{X} (u^1, u^2) = \boldsymbol{X} (u^1 + \mathrm{d} u^1, u^2 + \mathrm{d} u^2) - \boldsymbol{X} (u^1, u^2)
$$

上式右端的两个向量有不同的起点，它们能做减法的原因是，向量在欧氏空间$$\mathbb{E}^3$$中能够作平行移动，因而把这两个向量的起点移到同一点后再相减。但是，一般说来，向量$$\mathrm{d} \boldsymbol{X} (u^1, u^2)$$不再与曲面$$S$$相切了。实际上，对$$\boldsymbol{X} (u^1, u^2)$$求微分得到

$$
\begin{aligned}
\mathrm{d} \boldsymbol{X} (u^1, u^2) &= \mathrm{d} x^\alpha \boldsymbol{r}_\alpha + x^\alpha \mathrm{d} \boldsymbol{r}_\alpha \\
&= (\mathrm{d} x^\alpha + x^\beta \Gamma_{\beta \gamma}^\alpha \mathrm{d} u^\gamma ) \boldsymbol{r}_\alpha + x^\alpha \mathrm{d} u^\beta b_{\alpha \beta} \boldsymbol{n}
\end{aligned}
$$

要从$$\mathrm{d} \boldsymbol{X} (u^1, u^2)$$得到曲面$$S$$的切向量，只要取$$\mathrm{d} \boldsymbol{X} (u^1, u^2)$$的切分量，也就是将$$\mathrm{d} \boldsymbol{X} (u^1, u^2)$$在$$S$$的切空间上作正交投影。

**定义6.2** 命
$$
\mathrm{D} \boldsymbol{X} (u^1, u^2) = \big( \mathrm{d} \boldsymbol{X} (u^1, u^2) \big)^\top = ( \mathrm{d} x^\alpha + x^\beta \Gamma_{\beta \gamma}^\alpha \mathrm{d} u^\gamma ) \boldsymbol{r}_\alpha
$$
，其中$$\top$$表示将$$\mathbb{E}^3$$中的向量向曲面$$S$$在$$(u^1, u^2)$$的切空间作正交投影。称$$\mathrm{D} \boldsymbol{X} (u^1, u^2)$$为曲面$$S$$上的切向量场$$\boldsymbol{X} (u^1, u^2)$$的**协变微分**。
{:.success}

记

$$
\mathrm{D} x^\alpha = \mathrm{d} x^\alpha + x^\beta \Gamma_{\beta \gamma}^\alpha \mathrm{d} u^\gamma
$$

则协变微分可以表示为

$$
\mathrm{D} \boldsymbol{X} (u^1, u^2) = \mathrm{D} x^\alpha \ \boldsymbol{r}_\alpha
$$

我们称$$\mathrm{D} x^\alpha$$为切向量场$$\boldsymbol{X}$$的分量$$x^\alpha (u^1, u^2)$$的协变微分。

**定理6.14** 曲面$$S$$上的切向量场$$\boldsymbol{X}$$的协变微分在曲面$$S$$的保长变换下是保持不变的，即如果$$\sigma: S \rightarrow \tilde{S}$$是保长对应，则对曲面$$S$$上的任意一个可微的切向量场$$\boldsymbol{X}$$有$$\sigma_* (\mathrm{D} \boldsymbol{X}) = \mathrm{D} (\sigma_* \boldsymbol{X})$$。
{:.info}

**证明** 在曲面$$S$$和$$\tilde{S}$$上取适用的参数系，使得保长对应$$\sigma$$是曲面$$S$$和$$\tilde{S}$$上有相同参数值的点之间的对应，因而切映射$$\sigma_*$$把曲面$$S$$的自然基底向量映射为$$\tilde{S}$$的对应的自然基底向量。由于切映射$$\sigma_*$$是线性映射，所以切向量场$$\boldsymbol{X}$$和$$\sigma_* \boldsymbol{X}$$关于各自的自然基底有相同的分量$$x^\alpha (u^1, u^2)$$，即

$$
\boldsymbol{X} = x^\alpha (u^1, u^2) \boldsymbol{r}_\alpha , \ \ \ 
\sigma_* \boldsymbol{X} = x^\alpha (u^1, u^2) \tilde{\boldsymbol{r}}_\alpha
$$

因为$$\sigma$$是保长对应，故曲面$$S$$和$$\tilde{S}$$在适用的参数系下有相同的第一类基本量，因而有相同的Christoffel记号$$\Gamma_{\beta \gamma}^\alpha$$。根据协变微分的定义式，$$\mathrm{D} \boldsymbol{X}$$和$$\mathrm{D} (\sigma_* \boldsymbol{X})$$关于各自的自然切标架场有相同的分量，因此

$$
\mathrm{D} \boldsymbol{X} = ( \mathrm{d} x^\alpha + x^\beta \Gamma_{\beta \gamma}^\alpha \mathrm{d} u^\gamma ) \boldsymbol{r}_\alpha
$$

$$
\mathrm{D} (\sigma_* \boldsymbol{X}) = ( \mathrm{d} x^\alpha + x^\beta \Gamma_{\beta \gamma}^\alpha \mathrm{d} u^\gamma ) \tilde{\boldsymbol{r}}_\alpha = \sigma_* (\mathrm{D} \boldsymbol{X})
$$

证毕∎

由**定理6.14**可知，切向量场$$\boldsymbol{X}$$的协变微分是属于曲面的内蕴几何的概念，与曲面的第二基本形式无关。

实际上，在具有第一基本形式的抽象曲面$$S$$上能够定义可微的切向量场$$\boldsymbol{X} (u^1, u^2) = x^\alpha (u^1, u^2) \boldsymbol{r}_\alpha (u^1, u^2)$$的协变微分

$$
\mathrm{D} \boldsymbol{X} (u^1, u^2) = ( \mathrm{d} x^\alpha + x^\beta \Gamma_{\beta \gamma}^\alpha \mathrm{d} u^\gamma ) \boldsymbol{r}_\alpha
$$

其中$$\Gamma_{\beta \gamma}^\alpha$$是曲面$$S$$的第一类基本量的Christoffel记号。

**定理6.15** 曲面$$S$$上的可微切向量场的协变微分有下列运算法则：  
(1) $$\mathrm{D} ( \boldsymbol{X} + \boldsymbol{Y} ) = \mathrm{D} \boldsymbol{X} + \mathrm{D} \boldsymbol{Y}$$  
(2) $$\mathrm{D} ( f \cdot \boldsymbol{X} ) = \mathrm{d} f \cdot \boldsymbol{X} + f \cdot \mathrm{D} \boldsymbol{X}$$  
(3) $$\mathrm{d} ( \boldsymbol{X} \cdot \boldsymbol{Y} ) = \mathrm{D} \boldsymbol{X} \cdot \boldsymbol{Y} + \boldsymbol{X} \cdot \mathrm{D} \boldsymbol{Y}$$  
其中$$\boldsymbol{X}$$，$$\boldsymbol{Y}$$是曲面$$S$$上的可微切向量场，$$f$$是定义在曲面$$S$$上的可微函数。
{:.info}

**定理6.15**说明，协变微分$$\mathrm{D}$$具有普通微分$$\mathrm{d}$$所具有的相同的运算法则。

### 协变导数

设$$C: u^\alpha = u^\alpha (t)$$是曲面$$S$$上的一条曲线，假定$$\boldsymbol{X} (t)$$是曲面$$S$$上沿曲线$$C$$定义的一个切向量场。先假定$$S$$是空间$$\mathbb{E}^3$$中的一张曲面，那么$$\frac{\mathrm{d} \boldsymbol{X} (t)}{\mathrm{d} t}$$是空间$$\mathbb{E}^3$$中沿曲线$$C$$定义的一个向量场，一般说来，它不是曲面$$S$$上沿曲线$$C$$定义的切向量场。要从$$\frac{\mathrm{d} \boldsymbol{X} (t)}{\mathrm{d} t}$$得到曲面$$S$$上沿曲线$$C$$定义的切向量场，只要将它正交投影到曲面$$S$$在相应的点的切空间就行了。

**定义6.3** 命
$$
\frac{\mathrm{D} \boldsymbol{X} (t)}{\mathrm{d} t} = \bigg( \frac{\mathrm{d} \boldsymbol{X} (t)}{\mathrm{d} t} \bigg)^\top
$$
，我们把$$\frac{\mathrm{D} \boldsymbol{X} (t)}{\mathrm{d} t}$$称为曲面$$S$$上沿曲线$$C$$定义的切向量场$$\boldsymbol{X} (t)$$沿曲线$$C$$的**协变导数**。
{:.success}

若设

$$
\boldsymbol{X} (t) = x^\alpha (t) \boldsymbol{r}_\alpha (u^1 (t), u^2 (t))
$$

则有

$$
\begin{aligned}
\frac{\mathrm{d} \boldsymbol{X} (t)}{\mathrm{d} t} &= \frac{\mathrm{d} x^\alpha (t)}{\mathrm{d} t} \boldsymbol{r}_\alpha + x^\alpha (t) \frac{\partial \boldsymbol{r}_\alpha}{\partial u^\gamma} \frac{\mathrm{d} u^\gamma (t)}{\mathrm{d} t} \\
&= \bigg( \frac{\mathrm{d} x^\alpha (t)}{\mathrm{d} t} + \Gamma_{\beta \gamma}^\alpha x^\beta (t) \frac{\mathrm{d} u^\gamma (t)}{\mathrm{d} t} \bigg) \boldsymbol{r}_\alpha + b_{\alpha \gamma} x^\alpha (t) \frac{\mathrm{d} u^\gamma (t)}{\mathrm{d} t} \boldsymbol{n}
\end{aligned}
$$

因此

$$
\frac{\mathrm{D} \boldsymbol{X} (t)}{\mathrm{d} t} = \bigg( \frac{\mathrm{d} \boldsymbol{X} (t)}{\mathrm{d} t} \bigg)^\top = \bigg( \frac{\mathrm{d} x^\alpha (t)}{\mathrm{d} t} + \Gamma_{\beta \gamma}^\alpha x^\beta (t) \frac{\mathrm{d} u^\gamma (t)}{\mathrm{d} t} \bigg) \boldsymbol{r}_\alpha
$$

若命

$$
\frac{\mathrm{D} x^\alpha (t)}{\mathrm{d} t} = \frac{\mathrm{d} x^\alpha (t)}{\mathrm{d} t} + \Gamma_{\beta \gamma}^\alpha x^\beta (t) \frac{\mathrm{d} u^\gamma (t)}{\mathrm{d} t}
$$

则

$$
\frac{\mathrm{D} \boldsymbol{X} (t)}{\mathrm{d} t} = \frac{\mathrm{D} x^\alpha (t)}{\mathrm{d} t} \boldsymbol{r}_\alpha
$$

我们把$$\frac{\mathrm{D} x^\alpha (t)}{\mathrm{d} t}$$称为沿曲线$$C$$定义的切向量场$$\boldsymbol{X} (t)$$的分量$$x^\alpha (t)$$沿曲线$$C$$的协变导数。

从$$\frac{\mathrm{D} \boldsymbol{X} (t)}{\mathrm{d} t}$$的表达式得知，若在具有第一基本形式的抽象曲面$$S$$上沿曲线$$C$$定义了切向量场$$\boldsymbol{X} (t)$$，则我们就能够定义它沿曲线$$C$$的协变导数。协变导数$$\frac{\mathrm{D} \boldsymbol{X} (t)}{\mathrm{d} t}$$在曲面$$S$$的保长变换下是不变的，并且协变导数算子$$\frac{\mathrm{D}}{\mathrm{d} t}$$具有**定理6.15**所叙述的运算法则。

类似地，如果曲面$$S$$上的可微切向量场$$\boldsymbol{X} (u^1, u^2)$$的分量是$$x^\alpha (u^1, u^2)$$，则同样可以定义它沿参数曲线的协变导数

$$
x_{, \gamma}^\alpha = \frac{\partial x^\alpha (u^1, u^2)}{\partial u^\gamma} + \Gamma_{\beta \gamma}^\alpha x^\beta (u^1, u^2)
$$

于是分量$$x^\alpha (u^1, u^2)$$的协变微分成为

$$
\mathrm{D} x^\alpha = x_{, \gamma}^\alpha \mathrm{d} u^\gamma
$$

### 平行移动

**定义6.4** 设$$\boldsymbol{X} (t)$$是曲面$$S$$上沿曲线$$C: u^\gamma = u^\gamma (t)$$定义的可微切向量场。如果$$\frac{\mathrm{D} \boldsymbol{X} (t)}{\mathrm{d} t} = \boldsymbol{0}$$，则称切向量场$$\boldsymbol{X} (t)$$沿曲线$$C$$是**平行**的。
{:.success}

由协变导数的定义可知，切向量场$$\boldsymbol{X} (t)$$沿曲线$$C$$平行的充分必要条件是，它的分量$$x^\alpha (t)$$满足常微分方程组

$$
\frac{\mathrm{d} x^\alpha (t)}{\mathrm{d} t} + \Gamma_{\beta \gamma}^\alpha x^\beta (t) \frac{\mathrm{d} u^\gamma (t)}{\mathrm{d} t} = 0
$$

这是一阶线性齐次常微分方程组。根据常微分方程组理论，对于给定的可微曲线$$C: u^\gamma = u^\gamma (t)$$，$$a \leq t \leq b$$，以及任意给定的初始值$$x_0^\alpha$$，方程组在区间$$[a, b]$$上有唯一的一组解$$x^\alpha = x^\alpha (t)$$使得$$x^\alpha (t_0) = x_0^\alpha$$，其中$$t_0$$是区间$$[a, b]$$中的任意一个固定点。我们把沿曲线$$C$$定义的切向量场

$$
\boldsymbol{X} (t) = x^\alpha (t) \boldsymbol{r}_\alpha \big( u^1 (t), u^2 (t) \big)
$$

称为曲面$$S$$在点$$\boldsymbol{r}_0 = \boldsymbol{r} (u^1 (t_0), u^2 (t_0))$$处的切向量$$\boldsymbol{X}_0 = x_0^\alpha \boldsymbol{r}_\alpha \big( u^1 (t_0), u^2 (t_0) \big)$$沿曲线$$C$$作**平行移动**产生的向量场。

因为常微分方程组是一阶线性齐次常微分方程组，所以它的解的全体构成一个向量空间，该向最空间与曲面$$S$$在点$$\boldsymbol{r}_0$$处的切空间线性同构。用几何的语言说，上述性质表明：曲面$$S$$上的切向量沿可微曲线$$C$$的平行移动在曲面$$S$$沿曲线$$C$$各点的切空间之间建立了线性同构。另外，根据**定理6.15**(3)，如果$$\boldsymbol{X} (t)$$，$$\boldsymbol{Y} (t)$$是曲面$$S$$上沿曲线$$C$$平行的切向量场，则

$$
\frac{\mathrm{d}}{\mathrm{d} t} \big( \boldsymbol{X} (t) \cdot \boldsymbol{Y} (t) \big) = \frac{\mathrm{D} \boldsymbol{X} (t)}{\mathrm{d} t} \cdot \boldsymbol{Y} (t) + \boldsymbol{X} (t) \cdot \frac{\mathrm{D} \boldsymbol{Y} (t)}{\mathrm{d} t} = 0
$$

这意味着$$\boldsymbol{X} (t) \cdot \boldsymbol{Y} (t)$$是常数，即切向量沿曲线$$C$$的平行移动保持切
向量的内积不变。特别地，切向量沿曲线$$C$$的平行移动保持切向量的长度不变。综上所述，我们有下面的定理：

**定理6.16** 设$$C: u^\gamma = u^\gamma (t)$$，$$a \leq t \leq b$$是曲面$$S$$上连接点$$A = (u^1(a), u^2(a))$$和点$$B = (u^1(b), u^2(b))$$的一条可微曲线。用$$\mathrm{P}_a^b$$表示曲面$$S$$上的切向量沿曲线$$C$$从$$t = a$$到$$t = b$$的平行移动，则
$$
\mathrm{P}_a^b: T_A S \rightarrow T_B S
$$
是从切空间$$T_A S$$到切空间$$T_B S$$的等距同构。
{:.info}

从协变导数的**定义6.3**可以直接得到下面的定理，它为构造曲面上的切向量沿曲线的平行移动提供了一条有效途径。

**定理6.17** 设空间$$\mathbb{E}^3$$中两个曲面$$S_1$$和$$S_2$$相切，曲面$$S_1$$和$$S_2$$沿曲线$$C: u^\gamma = u^\gamma (t)$$的协变导数算子分别记为$$\frac{\mathrm{D}^{(1)}}{\mathrm{d} t}$$和$$\frac{\mathrm{D}^{(2)}}{\mathrm{d} t}$$。设$$\boldsymbol{X} (t)$$是这两个曲面沿曲线$$C$$定义的切向量场，则$$\frac{\mathrm{D}^{(1)} \boldsymbol{X} (t)}{\mathrm{d} t} = \frac{\mathrm{D}^{(2)} \boldsymbol{X} (t)}{\mathrm{d} t}$$。特别是，如果$$\boldsymbol{X}(t)$$作为曲面$$S_1$$上沿曲线$$C$$的切向量场是平行的，则它作为曲面$$S_2$$上沿曲线$$C$$的切向量场也是平行的。
{:.info}

一般来说，当切向量在曲面$$S$$上沿一条封闭曲线平行移动一周时所得到的切向量与原切向量未必是重合的。这是弯曲曲面上的几何学与欧氏平面几何学的本质差别。

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/g2VEqkW.png" width="80%">
</div>

在有了协变导数的概念之后，曲线的测地曲率的表达式和平面曲线的相对曲率的表达式就统一起来了。设曲面$$S$$上的曲线$$C$$的参数方程是$$u^\gamma = u^\gamma (s)$$，其中$$s$$是弧长参数，则曲线$$C$$的测地曲率是

$$
\begin{aligned}
\kappa_g &= \frac{\mathrm{d}^2 \boldsymbol{r}}{\mathrm{d} s^2} \cdot \boldsymbol{e}_2 (s) = \frac{\mathrm{D} \boldsymbol{e}_1 (s)}{\mathrm{d} s}  \cdot \boldsymbol{e}_2 (s) \\
&=
\sqrt{g_{11} g_{22} - (g_{12})^2}
\begin{vmatrix}
\frac{\mathrm{d} u^1}{\mathrm{d} s} & \frac{\mathrm{d} u^2}{\mathrm{d} s} \\
\frac{\mathrm{D}}{\mathrm{d} s} \big( \frac{\mathrm{d} u^1}{\mathrm{d} s} \big) & \frac{\mathrm{D}}{\mathrm{d} s} \big( \frac{\mathrm{d} u^2}{\mathrm{d} s} \big) \\
\end{vmatrix}
\end{aligned}
$$

对于在笛卡儿直角坐标系下的平面$$\mathbb{R}^2$$，其协变导数$$\frac{\mathrm{D}}{\mathrm{d} s}$$就是普通导数$$\frac{\mathrm{d}}{\mathrm{d} s}$$，于是上面的公式称为平面$$\mathbb{R}^2$$上曲线$$C$$的相对曲率$$\kappa_r$$的公式。

特别地，测地线的微分方程成为

$$
\frac{\mathrm{D}}{\mathrm{d} s} \bigg( \frac{\mathrm{d} \boldsymbol{r} (s)}{\mathrm{d} s} \bigg) = 0
$$

或者

$$
\frac{\mathrm{D}}{\mathrm{d} s} \bigg( \frac{\mathrm{d} u^\alpha}{\mathrm{d} s} \bigg) = 0
$$

所以，曲面$$S$$上的测地线$$C$$就是其单位切向量在曲面$$S$$上沿该曲线$$C$$自身平行的曲线，或者说曲面$$S$$上的测地线$$C$$就是该曲面$$S$$上的自平行曲线。在平面上，直线可以描述为其切方向不变的曲线。因此，在这个意义上，曲面上的测地线的概念也是平面上的直线概念的推广。

## 抽象曲面

在本章已经对于抽象曲面片上的微分几何进行了研究。具体地讲，所谓的抽象曲面片是指二维欧氏空间$$\mathbb{E}^2$$中的一个开区域$$D$$，并且在其中给定了一个正定的二次微分形式

$$
\mathrm{I} = g_{\alpha \beta} \mathrm{d} u^\alpha \mathrm{d} u^\beta
$$

其中求和指标$$\alpha$$、$$\beta$$取值为$$\alpha, \beta = 1, 2$$，$$g_{\alpha \beta} = g_{\beta \alpha}$$是$$D$$上的光滑函数，并且矩阵$$(g_{\alpha \beta})$$在$$D$$内是处处正定的。它就是熟知的曲面的第一基本形式，或称为度量形式，其几何意义是分量为$$( \mathrm{d} u^1, \mathrm{d} u^2)$$的切向量的长度平方。所谓的在抽象曲面片$$(D, \mathrm{I})$$上的微分几何是指在本章中所论述的只与第一基本形式有关的几何量和几何概念，例如Gauss曲率$$K$$，区域$$D$$中一条曲线的长度和测地曲率，区域$$D$$中曲线长度的变分公式及测地线测地坐标系和法坐标系，区域$$D$$内的切向量沿一条光滑曲线的平行移动，等等。

需要指出的是，在本章前面的叙述中，往往是从三维欧氏空间$$\mathbb{E}^3$$中一张"具体的"参数曲面片出发，分析出那些不依赖曲面的第二基本形式、而只与曲面的第一基本形式有关的几何量和几何概念，因此在引入这些概念的过程中显得有点繁杂，而不是那么直截了当的。在另一方面，我们还只局限千一个坐标域内，即局限在一个曲面片上，缺乏对于抽象曲面的整体性的描述和了解。因此，在这一节，我们首先要引进整体的抽象曲面的概念，然后讨论该抽象曲面上的几何概念和几何性质。

### 二维流形

从[定义3.1](/2023/10/18/DifferentialGeometry-NOTES-03.html#正则曲面)得到启发，所谓的整体的抽象曲面是一些参数曲面片粘合的结果，要求两个参数曲面片$$(U_i; (u_i^1, u_i^2))$$和$$(U_j; (u_j^1, u_j^2))$$在其交集$$U_i \cap U_j \neq \varnothing$$的情况下，坐标变换

$$
u_i^\alpha = u_i^\alpha (u_j^1, u_j^2), \ \ \ u_j^\alpha = u_j^\alpha (u_i^1, u_i^2), \ \ \ \alpha = 1, 2
$$

都是$$C^\infty$$函数，并且坐标变换的Jacobi矩阵
$$
\begin{pmatrix}
\frac{\partial u_i^1}{\partial u_j^1} & \frac{\partial u_i^2}{\partial u_j^1} \\
\frac{\partial u_i^1}{\partial u_j^2} & \frac{\partial u_i^2}{\partial u_j^2} \\
\end{pmatrix}
$$
以及
$$
\begin{pmatrix}
\frac{\partial u_j^1}{\partial u_i^1} & \frac{\partial u_j^2}{\partial u_i^1} \\
\frac{\partial u_j^1}{\partial u_i^2} & \frac{\partial u_i^2}{\partial u_i^2} \\
\end{pmatrix}
$$
都是可逆矩阵，并且互为逆矩阵。

更为正式的定义是：设$$M$$是一个拓扑空间(因而在$$M$$中有开集的结构，以及连续函数和连续映射的概念)。如果对于每一点$$p \in M$$都存在点$$p$$的一个开邻域$$U$$和$$\mathbb{R}^2$$中的一个开区域$$D$$, 以及从$$D$$到$$U$$的同胚$$\varphi: D \rightarrow U$$(即$$\varphi$$是从$$D$$到$$U$$的一一对应，并且$$\varphi$$以及它的逆映射都是连续的)，则称$$M$$是一个**二维拓扑流形**。这里的$$(U, \varphi)$$称为$$M$$的一个**坐标卡**。对于任意一点$$p \in U$$，命

$$
u^\alpha (p) = \big( \varphi^{-1} (p) \big)^\alpha, \ \ \ \alpha = 1, 2
$$

则称$$(u^1 (p), u^2 (p))$$为点$$p$$的坐标，而称$$(U; (u^1, u^2))$$为$$M$$的一个坐标系。

假定$$M$$是一个二维拓扑流形。如果存在$$M$$的坐标卡组成的一个集合$$\{ (U_i, \varphi_i): i \in I \}$$，使得

(1) $$\{ U_i: i \in I \}$$是$$M$$的一个开覆盖；  
(2) 对于任意的$$i, j \in I$$，当$$U_i \cap U_j \neq \varnothing$$时，要求映射$$\varphi_j^{-1} \circ \varphi_i: \varphi_i^{-1} (U_i \cap U_j) \rightarrow \varphi_j^{-1} (U_i \cap U_j)$$和$$\varphi_i^{-1} \circ \varphi_j: \varphi_j^{-1} (U_i \cap U_j) \rightarrow \varphi_i^{-1} (U_i \cap U_j)$$都是$$C^\infty$$的；

则称$$M$$是一个**二维光滑流形**。

映射$$\varphi_j^{-1} \circ \varphi_i$$正是前面所说的坐标变换。实际上，对于任意的$$p \in U_i \cap U_j$$，我们有

$$
\varphi_j^{-1} \circ \varphi_i (u_i^1 (p), u_i^2 (p)) = \varphi_j^{-1} \circ \varphi_i (\varphi_i^{-1} (p)) = \varphi_j^{-1} (p) = (u_j^1 (p), u_j^2 (p))
$$

### 切向量

对于$$\mathbb{E}^3$$的曲面而言，切向量是一个十分直观的概念。对于二维光滑流形来说，切向量的概念引进却颇费周折。我们采取以下的定义：设$$p \in M$$，所谓$$M$$在点$$p$$的一个**切向量**$$\boldsymbol{v}$$是指在包含点$$p$$的每一个容许的坐标卡$$(U_i, \varphi_i)$$下，$$\boldsymbol{v}$$对应于一组数$$(v_i^1, v_i^2)$$，并且当$$(U_i, \varphi_i)$$和$$(U_j, \varphi_j)$$是包含点$$p$$的任意两个容许的坐标卡时，对应的数组$$(v_i^1, v_i^2)$$和$$(v_j^1, v_j^2)$$满足以下的关系式：

$$
v_j^\alpha = v_i^\beta \cdot \frac{\partial u_j^\alpha}{\partial u_i^\beta} \bigg\vert_p, \ \ \ \alpha = 1, 2
$$

这里，$$\alpha, \beta = 1, 2$$是求和指标，$$i$$、$$j$$是标记不同坐标卡的记号，不做求和用，以下都遵从这样的规定。换言之，切向量在各个坐标卡下对应的数组之间是线性变换关系，而该线性变换的矩阵恰好是坐标变换的Jacobi矩阵。

二维光滑流形$$M$$在点$$p$$的切向量$$\boldsymbol{v}$$能够解释为在点$$p$$的微分算子$$\boldsymbol{v}: C_p^\infty \rightarrow \mathbb{R}$$，这里$$C_p^\infty$$是指在点$$p$$的某个开邻域有定义、并且有各阶连续可微偏导数的函数的集合，该微分算子的定义是

$$
\boldsymbol{v} (f) = v_i^\alpha \cdot \frac{\partial (f \circ \varphi_i)}{\partial u_i^\alpha} \bigg\vert_{\varphi_i^{-1} (p)}, \ \ \ \forall f \in C_p^\infty
$$

上述定义与含有点$$p$$的容许坐标卡$$(U_i, \varphi_i)$$的选择无关。实际上，若$$(U_j, \varphi_j)$$是另一个含有点$$p$$的容许坐标卡，则根据求偏导数的链式法则得到

$$
\begin{aligned}
v_j^\alpha \cdot \frac{\partial (f \circ \varphi_j)}{\partial u_j^\alpha} \bigg\vert_{\varphi_j^{-1} (p)} 
&= v_j^\alpha \cdot \frac{\partial \big( (f \circ \varphi_i) \circ (\varphi_i^{-1} \circ \varphi_j) \big)}{\partial u_j^\alpha} \bigg\vert_{\varphi_j^{-1} (p)} \\
&= v_j^\alpha \cdot \frac{\partial (f \circ \varphi_i)}{\partial u_i^\beta} \bigg\vert_{\varphi_i^{-1} (p)} \cdot \frac{\partial (\varphi_i^{-1} \circ \varphi_j)^\beta}{\partial u_j^\alpha} \bigg\vert_{\varphi_j^{-1} (p)} \\
&= v_i^\beta \cdot \frac{\partial (f \circ \varphi_i)}{\partial u_i^\beta} \bigg\vert_{\varphi_i^{-1} (p)}
\end{aligned}
$$

不难验证，微分算子$$\boldsymbol{v}: C_p^\infty \rightarrow \mathbb{R}$$遵从以下两个法则：

(1) $$\boldsymbol{v} (f + \lambda g) = \boldsymbol{v} (f) + \lambda \boldsymbol{v} (g)$$；  
(2) $$\boldsymbol{v} (f \cdot g) = f(p) \cdot \boldsymbol{v} (g) + g(p) \cdot \boldsymbol{v} (f)$$，$$\forall f, g \in C_p^\infty$$，$$\lambda \in \mathbb{R}$$

值得指出的是，若$$(U_i, \varphi_i)$$是$$M$$的一个坐标卡，则在$$U_i$$上定义好了两个向量场$$\frac{\partial}{\partial u_i^\alpha}: C^\infty (U_i) \rightarrow C^\infty (U_i)$$，$$\alpha = 1, 2$$，它们的定义是

$$
\frac{\partial}{\partial u_i^\alpha} (f) = \frac{\partial (f \circ \varphi_i)}{\partial u_i^\alpha}, \ \ \ \forall f \in C^\infty (U_i)
$$

很明显，这两个切向量场是处处线性无关的。实际上在坐标卡$$(U_i, \varphi_i)$$下，向量场$$\frac{\partial}{\partial u_i^1}$$对应于数组$$(1, 0)$$，向量场$$\frac{\partial}{\partial u_i^2}$$对应于数组$$(0, 1)$$。因此，$$\bigg\{ p; \frac{\partial}{\partial u_i^1}\bigg\vert_p, \frac{\partial}{\partial u_i^2}\bigg\vert_p \bigg\}$$是坐标域$$U_i$$内的标架场，称为$$U_i$$上的自然标架场。

### 度量形式

所谓的在二维光滑流形上$$M$$的一个度量形式$$g$$是指对于$$M$$的任意一个容许坐标卡$$(U_i, \varphi_i)$$，$$g$$在$$U_i$$上的限制是一个正定的二次微分形式

$$
g \vert_{U_i} = g_{\alpha \beta}^{(i)} \mathrm{d} u_i^\alpha \mathrm{d} u_i^\beta
$$

其中$$g_{\alpha \beta}^{(i)} \in C^\infty (U_i)$$，且$$g_{\alpha \beta}^{(i)} = g_{\beta \alpha}^{(i)}$$，矩阵$$(g_{\alpha \beta}^{(i)})$$在$$U_i$$上是处处正定的。如果$$(U_j, \varphi_j)$$是另一个容许坐标卡，且$$U_i \cap U_j \neq \varnothing$$，则在交集$$U_i \cap U_j$$上有

$$
g \vert_{U_i \cap U_j} = g_{\alpha \beta}^{(i)} \mathrm{d} u_i^\alpha \mathrm{d} u_i^\beta = g_{\gamma \delta}^{(j)} \mathrm{d} u_j^\gamma \mathrm{d} u_j^\delta = g_{\gamma \delta}^{(j)} \frac{\partial u_j^\gamma}{\partial u_i^\alpha} \frac{\partial u_j^\delta}{\partial u_i^\beta} \mathrm{d} u_i^\alpha \mathrm{d} u_i^\beta
$$

这里的$$g_{\gamma \delta}^{(j)} \frac{\partial u_j^\gamma}{\partial u_i^\alpha} \frac{\partial u_j^\delta}{\partial u_i^\beta}$$关于下指标$$\alpha$$，$$\beta$$显然是对称的，因此有

$$
g_{\alpha \beta}^{(i)} = g_{\gamma \delta}^{(j)} \frac{\partial u_j^\gamma}{\partial u_i^\alpha} \frac{\partial u_j^\delta}{\partial u_i^\beta}, \ \ \ \alpha, \beta = 1, 2
$$

由此可见，$$M$$上的度量形式$$g$$实际上是在任意一个容许坐标卡$$(U_i, \varphi_i)$$下指定了一个由定义在区域$$U_i$$上的光滑函数构成的、对称的正定矩阵$$(g_{\alpha \beta}^{(i)})$$，并且当另一个容许坐标卡$$(U_j, \varphi_j)$$适合条件$$U_i \cap U_j \neq \varnothing$$时，相应的$$g_{\alpha \beta}^{(i)}$$和$$g_{\gamma \delta}^{(j)}$$在$$U_i \cap U_j$$上满足双重线性变换的关系式

$$
g_{\alpha \beta}^{(i)} = g_{\gamma \delta}^{(j)} \frac{\partial u_j^\gamma}{\partial u_i^\alpha} \frac{\partial u_j^\delta}{\partial u_i^\beta}, \ \ \ 1 \leq \alpha, \beta \leq 2
$$

我们把具有上述结构的量$$g$$称为2阶协变张量。

如在一个二维光滑流形$$M$$上指定了一个度量形式$$g$$，则称$$(M, g)$$是一个**二维黎曼流形**，这就是我们所要研究的抽象曲面。很明显，这种抽象曲面$$(M, g)$$就是一些抽象曲面片(或参数曲面片)粘合的结果。在这里，度量形式$$g$$有明确的几何意义：设$$\boldsymbol{v}$$是$$M$$在点$$p$$的一个切向量，$$(U_i, \varphi_i)$$是包含点$$p$$的一个容许坐标卡，假定$$\boldsymbol{v}$$对应于数组$$(v_i^1, v_i^2)$$，而$$g \vert_{U_i} = g_{\alpha \beta}^{(i)} \mathrm{d} u_i^\alpha \mathrm{d} u_i^\beta$$，命

$$
g\vert_p (\boldsymbol{v}, \boldsymbol{v}) = g_{\alpha \beta}^{(i)}\vert_p v_i^\alpha v_i^\beta
$$

则上式右端与坐标卡$$(U_i, \varphi_i)$$的选取无关，记$$g\vert_p (\boldsymbol{v}, \boldsymbol{v}) = \vert \boldsymbol{v} \vert^2$$。

实际上，若有另一个容许坐标卡$$(U_j, \varphi_j)$$，使得$$p \in U_j$$，则$$\boldsymbol{v}$$对应于数组$$(v_j^1, v_j^2)$$，而$$g\vert_{U_j} =  g_{\gamma \delta}^{(j)} \mathrm{d} u_j^\gamma \mathrm{d} u_j^\delta$$，那么

$$
v_j^\gamma = v_i^\alpha \cdot \frac{\partial u_j^\gamma}{\partial u_i^\alpha} \bigg\vert_p, \ \ \
g_{\alpha \beta}^{(i)}\vert_p = g_{\gamma \delta}^{(j)}\vert_p \frac{\partial u_j^\gamma}{\partial u_i^\alpha}\bigg\vert_p \frac{\partial u_j^\delta}{\partial u_i^\beta}\bigg\vert_p
$$

因此

$$
g_{\gamma \delta}^{(j)}\vert_p v_j^\gamma v_j^\delta =
g_{\gamma \delta}^{(j)}\vert_p \ \frac{\partial u_j^\gamma}{\partial u_i^\alpha} \bigg\vert_p \ \frac{\partial u_j^\delta}{\partial u_i^\beta} \bigg\vert_p v_i^\alpha v_i^\beta = 
g_{\alpha \beta}^{(i)}\vert_p v_i^\alpha v_i^\beta
$$

很明显，度量形式$$g$$在坐标卡$$(U_i, \varphi_i)$$下的矩阵$$(g_{\alpha \beta}^{(i)})$$正好是自然标架场$$\bigg\{ p; \frac{\partial}{\partial u_i^1}\bigg\vert_p, \frac{\partial}{\partial u_i^2}\bigg\vert_p \bigg\}$$的度量系数，即

$$
g_{\alpha \beta}^{(i)} = g\vert_{U_i} \bigg( \frac{\partial}{\partial u_i^1}, \frac{\partial}{\partial u_i^2} \bigg)
$$

## 抽象曲面上的几何学

假定$$(M, g)$$是一个抽象曲面，即$$(M, g)$$是一个二维黎曼流形。本节的目标是考察在$$(M, g)$$上有哪些几何内容可以进行研究。

### 在$$(M, g)$$上光滑曲线的长度

### $$(M, g)$$上的一个紧致闭区域的面积

### $$(M, g)$$上的切向量场的协变微分

### 切向量沿光滑曲线的平行移动

### $$(M, g)$$中曲线的测地曲率

### $$(M, g)$$中的测地线

## 抽象曲面的曲率

## Gauss-Bonnet公式
---
layout: article
title: 微分几何笔记02-曲线论
tags: ["CG", "Geometry Processing", "Math"]
key: DifferentialGeometry-02
aside:
  toc: true
sidebar:
  nav: DifferentialGeometry
---

> 这个系列是北京大学陈维桓教授《微分几何(第二版)》的学习笔记，主要涉及古典微分几何中曲线曲面理论的相关知识。系统学习微分几何对于理解计算机图形学中的各种几何处理算法是十分有益的。
<!--more-->

## 正则参数曲线

### 参数曲线

首先我们来介绍**曲线**的概念。在微分几何中我们认为$$\mathbb{E}^3$$中的曲线$$C$$是从区间$$[a, b]$$到$$\mathbb{E}^3$$的一个连续映射，记为

$$
p: [a, b] \rightarrow \mathbb{E}^3
$$

称为**参数曲线**。给定$$\mathbb{E}^3$$中的正交标架$$\{O; \boldsymbol{i}, \boldsymbol{j}, \boldsymbol{k} \}$$，则曲线$$C$$上的点$$p(t)$$等同于向量$$\overrightarrow{Op(t)}$$。令$$\boldsymbol{r}(t) = \overrightarrow{Op(t)}$$，则$$\boldsymbol{r}(t)$$可以表示为向量函数

$$
\boldsymbol{r}(t) = x(t) \ \boldsymbol{i} + y(t) \ \boldsymbol{j} + z(t) \ \boldsymbol{k}, \ \ t \in [a, b]
$$

记为

$$
\boldsymbol{r}(t) = (x(t), y(t), z(t)), \ \ t \in [a, b]
$$

其中$$t$$是曲线的参数，上式称为曲线$$C$$的**参数方程**。

### 曲线的切线

根据导数定义可知

$$
\boldsymbol{r}'(t) = \lim_{\Delta t \to 0} \frac{\boldsymbol{r}(t + \Delta t) - \boldsymbol{r}(t)}{\Delta t} = (x'(t), y'(t), z'(t))
$$

如果坐标函数$$x'(t)$$，$$y'(t)$$，$$z'(t)$$是连续可微的，则称曲线$$\boldsymbol{r}(t)$$是连续可微的。这个概念与笛卡尔坐标系的选取无关。

导数$$\boldsymbol{r}'(t)$$有明显的几何意义。$$\boldsymbol{r}(t + \Delta t) - \boldsymbol{r}(t)$$表示点$$\boldsymbol{r}(t)$$到点$$\boldsymbol{r}(t + \Delta t)$$的有向线段，因此$$\frac{\boldsymbol{r}(t + \Delta t) - \boldsymbol{r}(t)}{\Delta t}$$表示经过点$$\boldsymbol{r}(t)$$和点$$\boldsymbol{r}(t + \Delta t)$$的割线$$l$$方向向量。当$$\Delta t \to 0$$时，割线$$l$$的极限位置就是曲线在点$$\boldsymbol{r}(t)$$处的**切线**。如果$$\boldsymbol{r}'(t) \neq \boldsymbol{0}$$，则$$\boldsymbol{r}'(t)$$是曲线在点$$\boldsymbol{r}(t)$$处的切线的方向向量，称为曲线的**切向量**如下图所示。

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/zIFDBhi.png" width="80%">
</div>

此时曲线在点$$\boldsymbol{r}(t)$$处的切线是可以完全确定的，这样的点称为曲线的**正则点**。而曲线在正则点处的切线方程为

$$
\boldsymbol{X}(u) = \boldsymbol{r}(t) + u \boldsymbol{r}'(t)
$$

其中$$t$$是固定的，$$u$$是切线上点的参数，$$\boldsymbol{X}(u)$$是从原点$$O$$指向切线上参数为$$u$$的点的有向线段。

### 正则参数曲线

我们称参数曲线$$\boldsymbol{r}(t)$$为**正则参数曲线**当且仅当它满足以下两个条件：

(1) $$\boldsymbol{r}(t)$$至少是自变量$$t$$的三次以上连续可微函数 *(曲线的几何不变量涉及$$\boldsymbol{r}(t)$$的三次导数)*

(2) 处处是正则点，即对任意的$$t$$有$$\boldsymbol{r}'(t) \neq \boldsymbol{0}$$

我们把参数$$t$$增大的方向称为该参数曲线的正向，因此$$\boldsymbol{r}'(t)$$正好指向曲线的正向。

### 参数变换

显然曲线参数方程的表达式与坐标系的选取有关，另外在固定的笛卡尔直角坐标系下还可以对参数进行一些变换。为了保证正则参数曲线的两个条件在参数变换下保持不变，我们要求参数变换$$t = t(u)$$需要满足以下两个条件：

(1) $$t(u)$$是$$u$$的三次以上连续可微函数

(2) $$t'(u)$$处处不为$$0$$

这样在参数变换$$t = t(u)$$下，曲线的参数方程可以表示为$$\boldsymbol{r} (t(u))$$，简记为$$\boldsymbol{r}(u)$$。根据求导的链式法则有

$$
\boldsymbol{r}'(u) = \frac{d}{d u} \boldsymbol{r}(t(u)) = \boldsymbol{r}'(t(u)) \cdot t'(u)
$$

如果容许的参数变换还要求$$t'(u) \gt 0$$，则这种容许的参数变换保持曲线的定向不变。

## 曲线的弧长

设$$\mathbb{E}^3$$中的一条正则曲线$$C$$的参数方程为$$\boldsymbol{r} = \boldsymbol{r}(t)$$，$$t \in [a, b]$$，我们定义

$$
s = \int_a^b \vert \boldsymbol{r}'(t) \vert \ dt
$$

则$$s$$是该曲线的一个不变量，即它与$$\mathbb{E}^3$$中笛卡尔直角坐标系的选取无关，也与该曲线的保持定向的容许参数变换无关。这里简单证明一下$$s$$对于保持定向的参数变换不变：

设参数变换为

$$
t = t(u), \ \ t'(u) \gt 0, \ \ u \in [\alpha, \beta]
$$

并且

$$
t(\alpha) = a, \ \ t(\beta) = b
$$

因此

$$
\bigg\vert \frac{d \boldsymbol{r}(t(u))}{du} \bigg\vert = \bigg\vert \frac{d\boldsymbol{r}}{dt}(t(u)) \bigg\vert \cdot \frac{d t}{d u}
$$

根据积分变量替换公式有

$$
\int_a^b \bigg\vert \frac{d \boldsymbol{r}(t)}{dt} \bigg\vert \ dt 
= \int_\alpha^\beta \bigg\vert \frac{d\boldsymbol{r}}{dt}(t(u)) \bigg\vert \cdot \frac{dt}{du} \ du 
= \int_\alpha^\beta \bigg\vert \frac{d \boldsymbol{r}(t(u))}{du} \bigg\vert \ du
$$

因此$$s$$与参数变换无关。

不变量$$s$$的几何意义是该曲线的长度。可以证明对于对于区间$$[a, b]$$的任意一个分割$$a = t_0 \lt t_1 \lt ... \lt t_n = b$$，下面的极限成立：

$$
\lim_{\lambda \to 0} \sum_{i=1}^n \vert \boldsymbol{r}(t_i) - \boldsymbol{r}(t_{i-1}) \vert = \int_a^b \vert \boldsymbol{r}'(t) \vert \ dt
$$

$$
\lambda = \max \{ \vert \Delta t_i \vert ; \ i = 1, ..., n \}
$$

不难发现等式的左端$$\sum_{i=1}^n \vert \boldsymbol{r}(t_i) - \boldsymbol{r}(t_{i-1}) \vert$$是顶点依次$$\boldsymbol{r}(t_0)$$，$$\boldsymbol{r}(t_1)$$，...，$$\boldsymbol{r}(t_n)$$为的折线长度，因此$$\int_a^b \vert \boldsymbol{r}'(t) \vert \ dt$$表示将曲线进行不断细分所得到的折线段长度的极限，也就是曲线的长度，称为**弧长**。

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/5CSudyd.png" width="80%">
</div>

### 弧长参数

对任意$$a \leq t \leq b$$令

$$
s(t) = \int_a^t \vert \boldsymbol{r}'(t) \vert \ dt
$$

则$$s(t)$$是曲线$$C$$由$$a$$到$$t$$的弧长。由于$$s(t)$$是关于$$t$$的三次以上连续可微函数，并且

$$
\frac{d s(t)}{d t} = \vert \boldsymbol{r}'(t) \vert \gt 0
$$

于是我们可以把弧长作为正则曲线的参数，这种参数称为曲线的**弧长参数**。弧长参数由曲线本身确定到至多相差一个常数(这反映了度量曲线长度的起点不同)，与表示曲线的笛卡尔直角坐标系的选取无关，与曲线原来的参数取法也无关。对弧长参数进行微分可以得到

$$
ds = \vert \boldsymbol{r}'(t) \vert \ dt
$$

上式中$$ds$$也是曲线的不变量，称为曲线的**弧长元素**。

在大多数情况下我们都无法显式地写出弧长参数的表达式，因此判定已知参数$$t$$是否是弧长参数是十分重要的。我们可以使用如下定理来进行判断：

**定理 2.1** 设$$\boldsymbol{r} = \boldsymbol{r}(t) \ (a \leq t \leq b)$$是$$\mathbb{E}^3$$中的一条正则参数曲线，则$$t$$是它的弧长参数的充要条件是$$\vert \boldsymbol{r}'(t) \vert \equiv 1$$。
{:.info}

这里简单证明如下：当$$t$$为弧长参数$$s$$时有$$ds = dt$$，所以必有$$\vert \boldsymbol{r}'(t) \vert \equiv 1$$，反之亦然。

[定理2.1](/2023/07/31/DifferentialGeometry-NOTES-02.html#弧长参数)的几何意义是曲线以弧长为参数的充要条件是它的切向量场为单位向量场。

### 曲线的曲率和Frenet标架

设曲线$$C$$的方程是$$\boldsymbol{r}(s)$$，其中$$s$$是曲线的弧长参数。令$$\boldsymbol{\alpha}(s) = \boldsymbol{r}'(s)$$，则$$\boldsymbol{\alpha}(s)$$是曲线$$C$$在$$s$$处的方向向量，其方向变化的快慢反映了曲线的弯曲程度，我们可以使用$$\big\vert \frac{d \boldsymbol{\alpha}}{ds} \big\vert$$来衡量。

**定理 2.2** 设$$\boldsymbol{\alpha}(s)$$是曲线$$\boldsymbol{r}(s)$$的单位切向量场，$$s$$是弧长参数，用$$\Delta \theta$$表示切向量$$\boldsymbol{\alpha}(s + \Delta s)$$和$$\boldsymbol{\alpha}(s)$$之间的夹角，则
$$
\lim_{\Delta s \to 0} \bigg \vert \frac{\Delta \theta}{\Delta s} \bigg \vert = \big\vert \frac{d \boldsymbol{\alpha}}{ds} \big\vert
$$
{:.info}

[定理2.2](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的曲率和frenet标架)证明如下：把曲线$$C$$上所有的单位切向量$$\boldsymbol{\alpha}(s)$$平行移动，使它们的起点都放在原点$$O$$出，则这些切向量的端点便描出单位球面上的一条曲线，于是切向量$$\boldsymbol{\alpha}(s + \Delta s)$$和$$\boldsymbol{\alpha}(s)$$之间的夹角$$\Delta \theta$$是在单位球面上从$$\boldsymbol{\alpha}(s + \Delta s)$$到$$\boldsymbol{\alpha}(s)$$的大圆弧的弧长，而$$\boldsymbol{\alpha}(s + \Delta s) - \boldsymbol{\alpha}(s)$$正好是该角所对的弦长，所以

$$
\begin{aligned}
\bigg\vert \frac{d \boldsymbol{\alpha}}{ds} \bigg\vert &= \lim_{\Delta s \to 0} \frac{\vert \boldsymbol{\alpha}(s + \Delta s) - \boldsymbol{\alpha}(s) \vert}{\vert \Delta s \vert} \\
&= \lim_{\Delta s \to 0} \frac{2 \vert \sin \frac{\Delta \theta}{2} \vert}{\vert \Delta s \vert} \\
&= \lim_{\Delta s \to 0} \bigg\vert \frac{\Delta \theta}{\Delta s} \bigg\vert
\end{aligned}
$$

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/GhhlaS3.png" width="80%">
</div>

**定义2.1** 设曲线$$C$$的方程是$$\boldsymbol{r}(s)$$，其中$$s$$是曲线的弧长参数。令$$\kappa(s) = \big\vert \frac{d \boldsymbol{\alpha}}{ds} \big\vert = \vert \boldsymbol{r}''(s) \vert$$，则称$$\kappa(s)$$为曲线$$\boldsymbol{r}(s)$$在$$s$$处的**曲率**，并且称$$\frac{d \boldsymbol{\alpha}}{ds}$$为该曲线的**曲率向量**。
{:.success}

**定理2.3** 曲线$$C$$是一条直线当且仅当它的曲率$$\kappa(s) \equiv 0$$。
{:.info}

**定理2.3**可证明如下：直线$$C$$的参数方程为$$\boldsymbol{r}(s) = \boldsymbol{r}_0 + \boldsymbol{\alpha}_0 s$$，其中$$\boldsymbol{\alpha}$$是该直线的方向向量。因此有$$\boldsymbol{r}'(s) = \boldsymbol{\alpha}$$，$$\boldsymbol{r}''(s) = \boldsymbol{0}$$，故$$\kappa(s) = \vert \boldsymbol{0} \vert \equiv 0$$。上述推导是可逆的，即$$\kappa(s) \equiv 0$$蕴含着$$\boldsymbol{r}(s) = \boldsymbol{r}_0 + \boldsymbol{\alpha}_0 s$$。

把曲线$$C$$的切向量$$\boldsymbol{\alpha}(s)$$平行移动到原点$$O$$，其端点描绘出的曲线称为曲线$$C$$的**切线像**，它的参数方程为

$$
\boldsymbol{r} = \boldsymbol{\alpha}(s)
$$

一般来说$$s$$不再是切线像的弧长，而切线像的弧长为

$$
d \tilde{s} = \bigg\vert \frac{d\boldsymbol{\alpha}}{ds} \bigg\vert \ ds = \kappa(s) \ ds
$$

所以

$$
\kappa(s) = \frac{d \tilde{s}}{ds}
$$

这就是说，曲线的曲率$$\kappa(s)$$是曲线切线像的弧长元素与曲线弧长元素之比。

因为$$\vert \boldsymbol{\alpha}(s) \vert = 1$$，根据[定理1.3](/2023/07/30/DifferentialGeometry-NOTES-01.html#向量函数)可知$$\boldsymbol{\alpha}'(s) \cdot \boldsymbol{\alpha}(s) = 0$$，即$$\boldsymbol{\alpha}(s) \perp \boldsymbol{\alpha}'(s)$$，所以$$\boldsymbol{\alpha}'(s)$$是曲线$$C$$的一个法向量。如果$$\kappa(s) \neq 0$$，则向量$$\boldsymbol{\alpha}'(s)$$有完全确定的方向，将这个方向的单位向量记为$$\boldsymbol{\beta}(s)$$，称其为曲线$$C$$的**主法向量**。于是，曲率向量$$\boldsymbol{\alpha}'(s)$$可以表示为

$$
\boldsymbol{\alpha}'(s) = \kappa(s) \ \boldsymbol{\beta}(s)
$$

曲线的单位切向量$$\boldsymbol{\alpha}(s)$$和主法向量$$\boldsymbol{\beta}(s)$$唯一地确定了曲线的第二个法向量

$$
\boldsymbol{\gamma} (s) = \boldsymbol{\alpha}(s) \times \boldsymbol{\beta} (s)
$$

称其为曲线的**次法向量**。这样，在正则曲线上曲率$$\kappa(s)$$不为零的点有一个完全确定的右手单位正交标架$$\{ \boldsymbol{r}(s); \boldsymbol{\alpha}(s), \boldsymbol{\beta}(s), \boldsymbol{\gamma}(s) \}$$，它与表示曲线的笛卡尔直角坐标系的选取无关，也不受曲线作保持定向的容许参数变换的影响，称为曲线在该点的**Frenet标架**。

在曲率$$\kappa(s)$$不为零的点，Frenet标架$$\{ \boldsymbol{r}(s); \boldsymbol{\alpha}(s), \boldsymbol{\beta}(s), \boldsymbol{\gamma}(s) \}$$的三根轴分别称为曲线的**切线**，**主法线**和**次法线**，三个坐标面分别称为曲线的**法平面**(以$$\boldsymbol{\alpha}$$为法向量的平面)，**从切平面**(以$$\boldsymbol{\beta}$$为法向量的平面)和**密切平面**(以$$\boldsymbol{\gamma}$$为法向量的平面)，它们的方程分别为：

(1) 法平面：$$(\boldsymbol{X} - \boldsymbol{r}(s)) \cdot \boldsymbol{\alpha}(s) = 0$$  
(2) 从切平面：$$(\boldsymbol{X} - \boldsymbol{r}(s)) \cdot \boldsymbol{\beta}(s) = 0$$  
(3) 密切平面：$$(\boldsymbol{X} - \boldsymbol{r}(s)) \cdot \boldsymbol{\gamma}(s) = 0$$

其中$$\boldsymbol{X}$$是相应平面上动点的向径。

对于弧长参数表达的曲线$$\boldsymbol{r}(s)$$，其曲率和Frenet标架可以直接根据定义计算：

$$
\boldsymbol{\alpha}(s) = \boldsymbol{r}'(s)
$$

$$
\kappa(s) = \vert \boldsymbol{\alpha}'(s) \vert = \vert \boldsymbol{r}''(s) \vert
$$

如果$$\kappa(s) \neq 0$$，则有

$$
\boldsymbol{\beta} (s) = \frac{\boldsymbol{r}''(s)}{\vert \boldsymbol{r}''(s) \vert}
$$

$$
\boldsymbol{\gamma} (s) = \boldsymbol{\alpha} (s) \times \boldsymbol{\beta} (s) = \frac{\boldsymbol{r}'(s) \times \boldsymbol{r}''(s)}{\vert \boldsymbol{r}''(s) \vert}
$$

对于一般的参数$$t$$则可以按照下式进行计算：

$$
\boldsymbol{\alpha} (t) = \frac{\boldsymbol{r}' (t)}{\vert \boldsymbol{r}' (t) \vert}, \
\boldsymbol{r}' (t) = \vert \boldsymbol{r}' (t) \vert \cdot \boldsymbol{\alpha} (t)
$$

$$
\begin{aligned}
\boldsymbol{r}'' (t) &= \frac{d \vert \boldsymbol{r}' (t) \vert}{dt} \cdot \boldsymbol{\alpha} (t) + \vert \boldsymbol{r}' (t) \vert \cdot \frac{d \boldsymbol{\alpha} (t)}{ds} \cdot \frac{ds}{dt} \\
&= \frac{d \vert \boldsymbol{r}' (t) \vert}{dt} \cdot \boldsymbol{\alpha} (t) + \vert \boldsymbol{r}' (t) \vert^2 \cdot \kappa (t) \cdot \boldsymbol{\beta}(t)
\end{aligned}
$$

所以

$$
\begin{aligned}
\boldsymbol{r}'(t) \times \boldsymbol{r}''(t) &= \vert \boldsymbol{r}'(t) \vert^3 \cdot \kappa(t) \big( \boldsymbol{\alpha}(t) \times \boldsymbol{\beta}(t) \big) \\
&= \vert \boldsymbol{r}'(t) \vert^3 \cdot \kappa(t) \ \boldsymbol{\gamma}(t)
\end{aligned}
$$

整理后可以得到

$$
\kappa(t) = \frac{\vert \boldsymbol{r}'(t) \times \boldsymbol{r}''(t) \vert}{\vert \boldsymbol{r}'(t) \vert^3}
$$

$$
\boldsymbol{\gamma} (t) = \frac{\boldsymbol{r}'(t) \times \boldsymbol{r}''(t)}{\vert \boldsymbol{r}'(t) \times \boldsymbol{r}''(t) \vert}
$$

$$
\begin{aligned}
\boldsymbol{\beta} (t) &= \boldsymbol{\gamma}(t) \times \boldsymbol{\alpha} (t) \\
&= \frac{\vert \boldsymbol{r}'(t) \vert}{\vert \boldsymbol{r}'(t) \times \boldsymbol{r}''(t) \vert} \boldsymbol{r}''(t) - \frac{\boldsymbol{r}'(t) \cdot \boldsymbol{r}''(t)}{\vert \boldsymbol{r}'(t) \vert \cdot \vert \boldsymbol{r}'(t) \times \boldsymbol{r}''(t) \vert} \boldsymbol{r}'(t)
\end{aligned}
$$

### 曲线的挠率和Frenet公式

[上一节](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的曲率和frenet标架)介绍了曲线在一点切线和主法线张成的平面称为曲线的密切平面，它的法向是曲线的次法向量$$\boldsymbol{\gamma}$$。如果曲线本身落在一个平面内，则该平面就是曲线的密切平面，于是它的次法向量$$\boldsymbol{\gamma}$$是常向量；如果曲线不是平面曲线，则$$\boldsymbol{\gamma}$$必定不是常向量。根据**定理2.2**，单位切向量$$\boldsymbol{\alpha}$$关于弧长参数$$s$$的导数的长度$$\vert \boldsymbol{\alpha}'(s) \vert$$反映了曲线切线方向转动的快慢；同理，次法向量$$\boldsymbol{\gamma}$$关于弧长参数$$s$$的导数的长度$$\vert \boldsymbol{\gamma}'(s) \vert$$反映了曲线的密切平面方向转动的快慢，因而它刻画了曲线偏离平面曲线程度，反映了曲线扭曲的程度，即曲线的"挠率"。

### 曲线论基本定理


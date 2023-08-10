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

## 曲线的曲率和Frenet标架

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

## 曲线的挠率和Frenet公式

[上一节](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的曲率和frenet标架)介绍了曲线在一点切线和主法线张成的平面称为曲线的密切平面，它的法向是曲线的次法向量$$\boldsymbol{\gamma}$$。如果曲线本身落在一个平面内，则该平面就是曲线的密切平面，于是它的次法向量$$\boldsymbol{\gamma}$$是常向量；如果曲线不是平面曲线，则$$\boldsymbol{\gamma}$$必定不是常向量。根据**定理2.2**，单位切向量$$\boldsymbol{\alpha}$$关于弧长参数$$s$$的导数的长度$$\vert \boldsymbol{\alpha}'(s) \vert$$反映了曲线切线方向转动的快慢；同理，次法向量$$\boldsymbol{\gamma}$$关于弧长参数$$s$$的导数的长度$$\vert \boldsymbol{\gamma}'(s) \vert$$反映了曲线的密切平面方向转动的快慢，因而它刻画了曲线偏离平面曲线程度，反映了曲线扭曲的程度，即曲线的"挠率"。

因为$$\boldsymbol{\gamma} (s)$$是单位向量场，故$$\boldsymbol{\gamma}' (s) \perp \boldsymbol{\gamma} (s)$$。此外根据Frenet标架的定义有

$$
\boldsymbol{\gamma} = \boldsymbol{\alpha} \times \boldsymbol{\beta}
$$

$$
\boldsymbol{\alpha}'(s) \parallel \boldsymbol{\beta}(s)
$$

所以

$$
\begin{aligned}
\boldsymbol{\gamma}'(s) &= \boldsymbol{\alpha}' (s) \times \boldsymbol{\beta} (s) + \boldsymbol{\alpha} (s) \times \boldsymbol{\beta}' (s) \\
&= \boldsymbol{\alpha} (s) \times \boldsymbol{\beta}' (s)
\end{aligned}
$$

这说明$$\boldsymbol{\gamma}'(s) \perp \boldsymbol{\alpha} (s)$$。于是$$\boldsymbol{\gamma}'(s)$$必定是与$$\boldsymbol{\beta} (s)$$是共线的，不妨设

$$
\boldsymbol{\gamma}'(s) = -\tau \boldsymbol{\beta} (s)
$$

因此

$$
\tau(s) = -\boldsymbol{\gamma}'(s) \cdot \boldsymbol{\beta} (s)
$$

并且

$$
\vert \tau(s) \vert = \vert \boldsymbol{\gamma}'(s) \vert
$$

**定义2.2** 设$$\boldsymbol{\beta}$$和$$\boldsymbol{\gamma}$$分别是曲线$$C$$的主法向量和次法向量，其中$$s$$是弧长参数，则$$\tau(s) = -\boldsymbol{\gamma}'(s) \cdot \boldsymbol{\beta} (s)$$称为曲线$$C$$的**挠率**。
{:.success}

**定理2.4** 设曲线$$C$$不是直线，则它是平面曲线当且仅当它的挠率为零。
{:.info}

**证明** 前面已经证明过平面曲线的次法向量$$\boldsymbol{\gamma}$$是常向量，因此其挠率必为零；接下来证明挠率为零的曲线是平面曲线。设曲线$$C$$的参数方程为$$\boldsymbol{r} = \boldsymbol{r}(s)$$，$$s$$是弧长参数，并且$$\kappa(s) \neq 0$$，$$\tau(s) \equiv 0$$。此时曲线有确定的Frenet标架$$\{ \boldsymbol{r}(s); \boldsymbol{\alpha}(s), \boldsymbol{\beta}(s), \boldsymbol{\gamma}(s) \}$$，并且

$$
\boldsymbol{\gamma}'(s) = -\tau(s) \cdot \boldsymbol{\beta} (s) \equiv 0
$$

因此$$\boldsymbol{\gamma}(s) = \boldsymbol{\gamma}_0$$为常向量。由于

$$
0 = \boldsymbol{r}'(s) \cdot \boldsymbol{\gamma}(s) = \boldsymbol{r}'(s) \cdot \boldsymbol{\gamma}_0 = \frac{d}{ds} \big( \boldsymbol{r}(s) \cdot \boldsymbol{\gamma}_0 \big)
$$

所以

$$
\boldsymbol{r}(s) \cdot \boldsymbol{\gamma}_0 = \boldsymbol{r}(s_0) \cdot \boldsymbol{\gamma}_0
$$

$$
\big( \boldsymbol{r}(s) - \boldsymbol{r}(s_0) \big) \cdot \boldsymbol{\gamma}_0 = 0
$$

这说明曲线落在经过点$$\boldsymbol{r}(s_0)$$、以常向量$$\boldsymbol{\gamma}_0$$为法向量的平面内。证毕。

根据曲率、挠率和Frenet标架的定义，我们可以总结出如下公式：

$$
\begin{aligned}
\boldsymbol{r}'(s) &= \boldsymbol{\alpha}(s) \\
\boldsymbol{\alpha}'(s) &= \kappa(s) \boldsymbol{\beta}(s) \\
\boldsymbol{\gamma}'(s) &= -\tau(s) \boldsymbol{\beta}(s)
\end{aligned}
$$

其中$$\boldsymbol{r}'(s)$$，$$\boldsymbol{\alpha}'(s)$$，$$\boldsymbol{\gamma}'(s)$$分别给出了Frenet标架的原点$$\boldsymbol{r}(s)$$和两个标架向量$$\boldsymbol{\alpha}(s)$$，$$\boldsymbol{\gamma}(s)$$的运动公式，要获得整个标架的运动公式只需要求出$$\boldsymbol{\beta}'(s)$$就行了。由于$$\{ \boldsymbol{r}(s); \boldsymbol{\alpha}(s), \boldsymbol{\beta}(s), \boldsymbol{\gamma}(s) \}$$是$$\mathbb{E}^3$$空间中的一个标架，所以$$\boldsymbol{\beta}'(s)$$一定可以表示为$$\boldsymbol{\alpha}(s)$$，$$\boldsymbol{\beta}(s)$$，$$\boldsymbol{\gamma}(s)$$的线性组合，不妨设

$$
\boldsymbol{\beta}'(s) = a \boldsymbol{\alpha}(s) + b \boldsymbol{\beta}(s) + c \boldsymbol{\gamma}(s)
$$

将上式分别与$$\boldsymbol{\alpha}(s)$$，$$\boldsymbol{\beta}(s)$$，$$\boldsymbol{\gamma}(s)$$进行点乘可以得到系数

$$
\begin{aligned}
a &= \boldsymbol{\beta}'(s) \cdot \boldsymbol{\alpha}(s) = -\boldsymbol{\beta}(s) \cdot \boldsymbol{\alpha}'(s) =-\kappa(s) \\
b &= \boldsymbol{\beta}'(s) \cdot \boldsymbol{\beta}(s)  = 0 \\
c &= \boldsymbol{\beta}'(s) \cdot \boldsymbol{\gamma}(s) = -\boldsymbol{\beta}(s) \cdot \boldsymbol{\gamma}'(s) = \tau(s) \\
\end{aligned}
$$

所以有

$$
\boldsymbol{\beta}'(s) = -\kappa(s) \boldsymbol{\alpha}(s) + \tau(s) \boldsymbol{\gamma}(s)
$$

总结一下可以得到Frenet标架$$\{ \boldsymbol{r}(s); \boldsymbol{\alpha}(s), \boldsymbol{\beta}(s), \boldsymbol{\gamma}(s) \}$$沿曲线$$C$$的运动公式

$$
\begin{cases}
\boldsymbol{r}'(s) &= \boldsymbol{\alpha}(s) \\
\boldsymbol{\alpha}'(s) &= \kappa(s) \boldsymbol{\beta}(s) \\
\boldsymbol{\beta}'(s) &= -\kappa(s) \boldsymbol{\alpha}(s) + \tau(s) \boldsymbol{\gamma}(s) \\
\boldsymbol{\gamma}'(s) &= -\tau(s) \boldsymbol{\beta}(s)
\end{cases}
$$

上述公式称为**Frenet公式**，是曲线论中最重要、最基本的公式。Frenet公式的后三个方程还可以写成矩阵的形式

$$
\begin{pmatrix}
\boldsymbol{\alpha}'(s) \\ \boldsymbol{\beta}'(s) \\ \boldsymbol{\gamma}'(s)
\end{pmatrix}
=
\begin{pmatrix}
0          & \kappa(s) & 0 \\
-\kappa(s) & 0         & \tau(s) \\
0          & -\tau(s)  & 0
\end{pmatrix}
\cdot
\begin{pmatrix}
\boldsymbol{\alpha}(s) \\ \boldsymbol{\beta}(s) \\ \boldsymbol{\gamma}(s)
\end{pmatrix}
$$

其中的系数矩阵为一个反对称矩阵，这不是Frenet标架的导数所特有的。实际上，沿曲线定义的任意一个单位正交标架场的导数公式的系数矩阵都是反对称的。

本节最后我们来推导挠率$$\tau(t)$$的计算公式。首先回忆次法向量$$\gamma(s)$$的计算公式

$$
\boldsymbol{\gamma} (t) = \frac{\boldsymbol{r}'(t) \times \boldsymbol{r}''(t)}{\vert \boldsymbol{r}'(t) \times \boldsymbol{r}''(t) \vert}
$$

等式左右两边对$$t$$进行求导可以得到

$$
\begin{aligned}
\boldsymbol{\gamma}' (t) 
&= \frac{d \boldsymbol{\gamma} (t)}{ds} \cdot \frac{ds}{dt} = -\tau(t) \boldsymbol{\beta}(t) \cdot \frac{ds}{dt} \\
&= \frac{\boldsymbol{r}'(t) \times \boldsymbol{r}'''(t)}{\vert \boldsymbol{r}'(t) \times \boldsymbol{r}''(t) \vert} + \frac{d}{dt} \bigg( \frac{1}{\vert \boldsymbol{r}'(t) \times \boldsymbol{r}''(t) \vert} \bigg) \cdot \big( \boldsymbol{r}'(t) \times \boldsymbol{r}''(t) \big)
\end{aligned}
$$

即

$$
-\tau(t) \boldsymbol{\beta}(t) \cdot \frac{ds}{dt} 
= \frac{\boldsymbol{r}'(t) \times \boldsymbol{r}'''(t)}{\vert \boldsymbol{r}'(t) \times \boldsymbol{r}''(t) \vert} + \frac{d}{dt} \bigg( \frac{1}{\vert \boldsymbol{r}'(t) \times \boldsymbol{r}''(t) \vert} \bigg) \cdot \big( \boldsymbol{r}'(t) \times \boldsymbol{r}''(t) \big)
$$

再对两边同时点乘$$\boldsymbol{\beta} (t)$$的计算式

$$
\boldsymbol{\beta} (t) = \frac{\vert \boldsymbol{r}'(t) \vert}{\vert \boldsymbol{r}'(t) \times \boldsymbol{r}''(t) \vert} \boldsymbol{r}''(t) - \frac{\boldsymbol{r}'(t) \cdot \boldsymbol{r}''(t)}{\vert \boldsymbol{r}'(t) \vert \cdot \vert \boldsymbol{r}'(t) \times \boldsymbol{r}''(t) \vert} \boldsymbol{r}'(t)
$$

最终得到

$$
\tau(t) = \frac{\big( \boldsymbol{r}'(t), \boldsymbol{r}''(t), \boldsymbol{r}'''(t) \big)}{ \vert \boldsymbol{r}'(t) \times \boldsymbol{r}''(t) \vert^2}
$$

如果$$t$$是弧长参数$$s$$，上式还可以简化为

$$
\tau(s) = \frac{\big( \boldsymbol{r}'(s), \boldsymbol{r}''(s), \boldsymbol{r}'''(s) \big)}{ \vert \boldsymbol{r}''(s) \vert^2}
$$

结合[定理2.4](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的挠率和frenet公式)，我们可以直接得到如下推论

**定理2.5** 曲线$$\boldsymbol{r} = \boldsymbol{r}(t)$$是一条平面曲线的充分必要条件是$$\big( \boldsymbol{r}'(s), \boldsymbol{r}''(s), \boldsymbol{r}'''(s) \big) \equiv 0$$。
{:.info}

## 曲线论基本定理

前面的讨论指出正则参数曲线的[弧长参数](/2023/07/31/DifferentialGeometry-NOTES-02.html#弧长参数)、[曲率](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的曲率和frenet标架)和[挠率](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的挠率和frenet公式)都是与曲线的保持定向的容许参数变换无关的，也与欧式空间$$\mathbb{E}^3$$中的笛卡尔直角坐标系的选取无关。当曲线在空间中经受一个刚体运动时，曲线的弧长、曲率和挠率是不变的；反过来说，如果空间$$\mathbb{E}^3$$中有两条曲线且它们的曲率和挠率表示成弧长参数的函数是分别相同的，则这两条曲线的形状是相同的。这个论断可以叙述成下面的基本定理。

**定理2.6** 设$$\boldsymbol{r} = \boldsymbol{r}_1(s)$$和$$\boldsymbol{r} = \boldsymbol{r}_2(s)$$是$$\mathbb{E}^3$$中两条以弧长$$s$$为参数的正则参数曲线。如果它们的曲率处处不为零，并且它们的曲率和挠率分别相等，即$$\boldsymbol{\kappa}_1 (s) =\boldsymbol{\kappa}_2 (s)$$，$$\boldsymbol{\tau}_1 (s) =\boldsymbol{\tau}_2 (s)$$，则有$$\mathbb{E}^3$$中的一个刚体运动$$\sigma$$，它把曲线$$\boldsymbol{r} = \boldsymbol{r}_1(s)$$变成曲线$$\boldsymbol{r} = \boldsymbol{r}_2(s)$$。
{:.info}

对于一般的参数曲线，上述定理还可以推导出如下结论。

**定理2.7** 设$$\boldsymbol{r} = \boldsymbol{r}_1(t)$$和$$\boldsymbol{r} = \boldsymbol{r}_2(u)$$是$$\mathbb{E}^3$$中两条正则参数曲线，它们的曲率处处不为零。如果存在三次以上的连续可微函数$$u = \lambda(t)$$，$$\lambda'(t) \neq 0$$，使得这两条曲线的弧长函数、曲率函数和挠率函数之间有关系式  
$$s_1(t) = s_2(\lambda(t))$$，
$$\kappa_1(t) = \kappa_2(\lambda(t))$$，
$$\tau_1(t) = \tau_2(\lambda(t))$$  
则有$$\mathbb{E}^3$$中的一个刚体运动$$\sigma$$，它把曲线$$\boldsymbol{r} = \boldsymbol{r}_1(t)$$变成曲线$$\boldsymbol{r} = \boldsymbol{r}_2(u)$$，即曲线$$\boldsymbol{r} = \boldsymbol{r}_2(\lambda(t))$$是曲线$$\boldsymbol{r} = \boldsymbol{r}_1(t)$$在刚体运动$$\sigma$$下的像。
{:.info}

### 曲线的内在方程

除此之外我们还知道在曲率$$\kappa(s)$$处处不为零的正则曲线上有内在的、确定的[Frenet标架场](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的曲率和frenet标架)，所以$$\mathbb{E}^3$$中的曲线便变成在$$\mathbb{E}^3$$中的正交标架空间中的一条曲线。而[Frenet公式](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的挠率和frenet公式)正好是这个标架场的运动方程，其系数恰好是曲线的曲率和挠率，它们完全确定了曲线在空间中的形状。我们的问题是：给定了曲率和挠率作为弧长参数$$s$$的函数$$\kappa(s)$$，$$\tau(s)$$后，在空间$$\mathbb{E}^3$$中是否存在正则参数曲线以给定的函数$$\kappa(s)$$，$$\tau(s)$$为它的曲率和挠率？我们在$$\mathbb{E}^3$$上由全体正交标架构成的六维空间中考虑，于是[Frenet公式](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的挠率和frenet公式)成为现成的已知常微分方程组，它的解是依赖参数$$s$$的一族正交标架，其标架原点在$$\mathbb{E}^3$$中描出的轨迹正是我们所需的曲线，而这族正交标架本身应该是曲线的Frenet标架场。

**定理2.8** 设$$\kappa(s)$$，$$\tau(s)$$是在区间$$[a, b]$$上两个任意给定的连续可微函数，并且$$\kappa(s) \lt 0$$，则在空间$$\mathbb{E}^3$$中存在正则参数曲线$$\boldsymbol{r} = \boldsymbol{r}(s)$$，$$a \leq s \leq b$$，以$$s$$为弧长参数，以给定的函数$$\kappa(s)$$，$$\tau(s)$$为它的曲率和挠率，且这样的曲线在$$\mathbb{E}^3$$中时完全确定的，其差异至多为曲线在空间中的位置不同。
{:.info}

**定理2.8**说明函数$$\kappa(s) \lt 0$$与$$\tau(s)$$在空间$$\mathbb{E}^3$$中不计位置的差异位于地确定了一条曲线，因此它们可以看作是该曲线的方程，称为曲线的**内在方程**或**自然方程**。从曲线的内在方程得到参数方程的过程可以表示为求解方程组

$$
\begin{cases}
\frac{d \boldsymbol{r}}{ds} = \boldsymbol{e}_1 \\
\frac{d \boldsymbol{e}_i}{ds} = \sum_{j=1}^3 a_{ij}(s) \boldsymbol{e}_j
\end{cases}
$$

其中$$\{ \boldsymbol{r}(s); \boldsymbol{e}_1(s), \boldsymbol{e}_2(s), \boldsymbol{e}_3(s) \}$$为曲线的Frenet标架，系数$$a_{ij}(s)$$需要满足

$$
\begin{pmatrix}
a_{11}(s) & a_{12}(s) & a_{13}(s) \\
a_{21}(s) & a_{22}(s) & a_{23}(s) \\
a_{31}(s) & a_{32}(s) & a_{33}(s) \\
\end{pmatrix}
=
\begin{pmatrix}
0          & \kappa(s) & 0 \\
-\kappa(s) & 0         & \tau(s) \\
0          & -\tau(s)  & 0
\end{pmatrix}
$$

而初始条件则为

$$
\boldsymbol{r}(s_0) = \boldsymbol{r}^0 , \
\boldsymbol{e}_i(s_0) = \boldsymbol{e}_i^0
$$

它是一个为右手单位正交标架，即满足条件

$$
\begin{cases}
\boldsymbol{e}^0_i(s) \cdot \boldsymbol{e}^0_j(s) = \delta_{ij}, \ 1 \leq i,j \leq 3 \\
\big( \boldsymbol{e}^0_1(s), \boldsymbol{e}^0_2(s), \boldsymbol{e}^0_3(s) \big) = 1
\end{cases}
$$

可以证明求解满足初始条件的常微分方程组得到的向量函数即为所需曲线。

显然在一般情况下求解曲线内在方程和常微分方程组来获得曲线的表达式是比较困难的，对于一些常见曲线我们总结了其内在方程有如下特征：

<center>

|         |  曲率$$\kappa(s)$$   | 挠率$$\tau(s)$$  |
|  :----:   |  :----:  | :----:  |
| 直线  | $$\kappa(s) \equiv 0$$ | - |
| 圆  | $$\kappa(s) \gt 0$$为常数 | $$\tau(s) \equiv 0$$ |
| 平面曲线  | - | $$\tau(s) \equiv 0$$ |
| 圆柱螺线  | $$\kappa(s) \gt 0$$为常数 | $$\kappa(s) \neq 0$$为常数 |

</center>

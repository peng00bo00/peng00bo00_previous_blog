---
layout: article
title: 微分几何笔记04-曲面的第二基本形式
tags: ["CG", "Geometry Processing", "Math", "Differential Geometry"]
key: DifferentialGeometry-04
aside:
  toc: true
sidebar:
  nav: DifferentialGeometry
---

> 这个系列是北京大学陈维桓教授《微分几何(第二版)》的学习笔记，主要涉及古典微分几何中曲线曲面理论的相关知识。系统学习微分几何对于理解计算机图形学中的各种几何处理算法是十分有益的。本节介绍曲面的第二基本形式。
<!--more-->

本节我们将研究描写正则参数曲面形状的方法，并且介绍曲面的各种曲率的概念。

## 第二基本形式

设$$S: \boldsymbol{r} = \boldsymbol{r} (u, v)$$是一张正则参数曲面。曲面$$S$$在任意一点$$(u_0, v_0)$$处的切平面$$\Pi$$的单位法向量是

$$
\boldsymbol{n} = \frac{\boldsymbol{r}_u \times \boldsymbol{r}_v}{\vert \boldsymbol{r}_u \times \boldsymbol{r}_v \vert} \bigg\vert_{(u_0, v_0)}
$$

在直观上，曲面$$S$$在点$$(u_0, v_0)$$处弯曲的状况可以用该点附近的点到切平面$$\Pi$$的有向距离$$\delta$$来刻画。若曲面$$S$$在点$$(u_0, v_0)$$处弯曲得越厉害，则$$\vert \delta \vert$$增加的速率越大，即$$\delta$$绝对值与邻近点到点$$(u_0, v_0)$$的距离之比反映了曲面在该邻近点方向的弯曲程度。$$\delta$$的符号说明曲面$$S$$上点$$(u_0, v_0)$$的邻近点落在点$$(u_0, v_0)$$的切平面$$\Pi$$的哪一侧。

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/0PCLU6u.png" width="80%">
</div>

设$$(u_0, v_0)$$的邻近点是$$(u_0 + \Delta u, v_0 + \Delta v)$$，它到切平面$$\Pi$$的有向距离是

$$
\delta (\Delta u, \Delta v) = (\boldsymbol{r} (u_0 + \Delta u, v_0 + \Delta v) - \boldsymbol{r} (u_0, v_0)) \cdot \boldsymbol{n}
$$

根据Taylor展开式有

$$
\begin{aligned}
(\boldsymbol{r} (u_0 + \Delta u, v_0 + \Delta v) - \boldsymbol{r} (u_0, v_0)) &= (\boldsymbol{r}_u \Delta u + \boldsymbol{r}_v \Delta v) \\
&+ \frac{1}{2} \big( \boldsymbol{r}_{uu} (\Delta u)^2 + 2 \boldsymbol{r}_{uv} \Delta u \Delta v + \boldsymbol{r}_{vv} (\Delta v)^2 \big) \\
&+ \boldsymbol{o} \big( (\Delta u)^2 + (\Delta v)^2 \big)
\end{aligned}
$$

其中向量函数$$\boldsymbol{r}_u$$，$$\boldsymbol{r}_{uu}$$等都在点$$(u_0, v_0)$$处取值，并且

$$
\lim_{(\Delta u)^2 + (\Delta v)^2 \rightarrow 0} \frac{\boldsymbol{o} \big( (\Delta u)^2 + (\Delta v)^2 \big)}{(\Delta u)^2 + (\Delta v)^2} = 0
$$

因此

$$
\begin{aligned}
\delta (\Delta u, \Delta v) &= \frac{1}{2} [L (\Delta u)^2 + 2 M \Delta u \Delta v + N (\Delta v)^2] \\
&+ \boldsymbol{o} \big( (\Delta u)^2 + (\Delta v)^2 \big)
\end{aligned}
$$

其中

$$
\begin{cases}
\begin{aligned}
L &= \boldsymbol{r}_{uu} (u_0, v_0) \cdot n (u_0, v_0) \\
M &= \boldsymbol{r}_{uv} (u_0, v_0) \cdot n (u_0, v_0) \\
N &= \boldsymbol{r}_{vv} (u_0, v_0) \cdot n (u_0, v_0) \\
\end{aligned}
\end{cases}
$$

由于$$\boldsymbol{r}_u \cdot \boldsymbol{n} = \boldsymbol{r}_v \cdot \boldsymbol{n} = 0$$，因此

$$
\begin{cases}
\begin{aligned}
\boldsymbol{r}_{uu} \cdot n + \boldsymbol{r}_u \cdot \boldsymbol{n}_u &= 0\\
\boldsymbol{r}_{uv} \cdot n + \boldsymbol{r}_u \cdot \boldsymbol{n}_v &= 0\\
\boldsymbol{r}_{vu} \cdot n + \boldsymbol{r}_u \cdot \boldsymbol{n}_u &= 0\\
\boldsymbol{r}_{vv} \cdot n + \boldsymbol{r}_u \cdot \boldsymbol{n}_v &= 0\\
\end{aligned}
\end{cases}
$$

所以$$L$$，$$M$$，$$N$$还能表示成

$$
\begin{cases}
\begin{aligned}
L &= -\boldsymbol{r}_{u} \cdot n_u \\
M &= -\boldsymbol{r}_{u} \cdot n_v = -\boldsymbol{r}_{v} \cdot n_u \\
N &= -\boldsymbol{r}_{v} \cdot n_v \\
\end{aligned}
\end{cases}
$$

这启示我们考虑二次微分式

$$
\begin{aligned}
\mathrm{II} &= (\mathrm{d}^2 \boldsymbol{r}) \cdot \boldsymbol{n} = - \mathrm{d} \boldsymbol{r} \cdot \mathrm{d} \boldsymbol{n} \\
&= L (\mathrm{d} u)^2 + 2M \mathrm{d} u \mathrm{d} v + N (\mathrm{d} v)^2
\end{aligned}
$$

上式称为曲面的**第二基本形式**，其系数$$L$$，$$M$$，$$N$$称为曲面的**第二类基本量**。

### 容许的参数变换

曲面的第二基本形式$$\mathrm{II}$$与第一基本形式$$\mathrm{I}$$有类似的特性，即与曲面上保持定向的容许参数变换是无关的。假定曲面有容许的参数变换

$$
\begin{cases}
\begin{aligned}
u &= u(\tilde{u}, \tilde{v}) \\ 
v &= v(\tilde{u}, \tilde{v}) \\ 
\end{aligned}
\end{cases}
$$

并且

$$
\frac{\partial (u, v)}{\partial (\tilde{u}, \tilde{v})} \gt 0
$$

因此

$$
\begin{cases}
\begin{aligned}
\boldsymbol{r}_{\tilde{u}} &= \boldsymbol{r}_u \frac{\partial u}{\partial \tilde{u}} + \boldsymbol{r}_v \frac{\partial v}{\partial \tilde{u}} \\
\boldsymbol{r}_{\tilde{v}} &= \boldsymbol{r}_u \frac{\partial u}{\partial \tilde{v}} + \boldsymbol{r}_v \frac{\partial v}{\partial \tilde{v}}
\end{aligned}
\end{cases}
$$

故

$$
\boldsymbol{r}_{\tilde{u}} \times \boldsymbol{r}_{\tilde{v}} = \frac{\partial (u, v)}{\partial (\tilde{u}, \tilde{v})} \boldsymbol{r}_u \times \boldsymbol{r}_v
$$

$$
\tilde{\boldsymbol{n}} = \boldsymbol{n}
$$

对法向量$$\tilde{\boldsymbol{n}}$$进行微分有

$$
\begin{cases}
\begin{aligned}
\tilde{\boldsymbol{n}}_{\tilde{u}} &= \boldsymbol{n}_u \frac{\partial u}{\partial \tilde{u}} + \boldsymbol{n}_v \frac{\partial v}{\partial \tilde{v}} \\
\tilde{\boldsymbol{n}}_{\tilde{v}} &= \boldsymbol{n}_u \frac{\partial u}{\partial \tilde{v}} + \boldsymbol{n}_v \frac{\partial v}{\partial \tilde{v}} \\
\end{aligned}
\end{cases}
$$

把它们写成矩阵的形式有

$$
\begin{pmatrix}
\boldsymbol{r}_{\tilde{u}} \\ \boldsymbol{r}_{\tilde{v}}
\end{pmatrix}
= J \cdot
\begin{pmatrix}
\boldsymbol{r}_{u} \\ \boldsymbol{r}_{v}
\end{pmatrix}
$$

$$
\begin{pmatrix}
\boldsymbol{n}_{\tilde{u}} \\ \boldsymbol{n}_{\tilde{v}}
\end{pmatrix}
= J \cdot
\begin{pmatrix}
\boldsymbol{n}_{u} \\ \boldsymbol{n}_{v}
\end{pmatrix}
$$

其中

$$
J = 
\begin{pmatrix}
\frac{\partial u}{\partial \tilde{u}} & \frac{\partial v}{\partial \tilde{u}} \\
\frac{\partial u}{\partial \tilde{v}} & \frac{\partial v}{\partial \tilde{v}} \\
\end{pmatrix}
$$

带入到第二基本形式的定义可以得到

$$
\begin{aligned}
\begin{pmatrix}
\tilde{L} & \tilde{M} \\ \tilde{M} & \tilde{N}
\end{pmatrix}
&=
-
\begin{pmatrix}
\boldsymbol{r}_{\tilde{u}} \\ \boldsymbol{r}_{\tilde{v}}
\end{pmatrix} \cdot
\begin{pmatrix}
\boldsymbol{n}_{\tilde{u}} & \boldsymbol{n}_{\tilde{v}}
\end{pmatrix} \\
&= -J \cdot
\begin{pmatrix}
\boldsymbol{r}_{u} \\ \boldsymbol{r}_{v}
\end{pmatrix} \cdot
\begin{pmatrix}
\boldsymbol{n}_{u} & \boldsymbol{n}_{v}
\end{pmatrix}
\cdot J^T \\
&= J 
\begin{pmatrix}
L & M \\ M & N
\end{pmatrix}
J^T
\end{aligned}
$$

由此可见，$$L$$，$$M$$，$$N$$在保持定向的容许参数变换下的变换规律与第一类基本量$$E$$，$$F$$，$$G$$的变换规律是一样的。很明显，根据函数微分的公式有

$$
\begin{pmatrix}
\mathrm{d} u & \mathrm{d} v
\end{pmatrix} = 
\begin{pmatrix}
\mathrm{d} \tilde{u} & \mathrm{d} \tilde{v}
\end{pmatrix}
\cdot J
$$

因此

$$
\begin{aligned}
L (\mathrm{d} u)^2 + 2M \mathrm{d} u \mathrm{d} v + N (\mathrm{d} v)^2 &=
\begin{pmatrix}
\mathrm{d} u & \mathrm{d} v
\end{pmatrix}
\begin{pmatrix}
L & M \\ M & N
\end{pmatrix}
\begin{pmatrix}
\mathrm{d} u \\ \mathrm{d} v
\end{pmatrix} \\
&=
\begin{pmatrix}
\mathrm{d} \tilde{u} & \mathrm{d} \tilde{v}
\end{pmatrix}
\cdot J
\begin{pmatrix}
L & M \\ M & N
\end{pmatrix}
J^T \cdot
\begin{pmatrix}
\mathrm{d} \tilde{u} \\ \mathrm{d} \tilde{v}
\end{pmatrix} \\
&= 
\begin{pmatrix}
\mathrm{d} \tilde{u} & \mathrm{d} \tilde{v}
\end{pmatrix}
\begin{pmatrix}
\tilde{L} & \tilde{M} \\ \tilde{M} & \tilde{N}
\end{pmatrix}
\begin{pmatrix}
\mathrm{d} \tilde{u} \\ \mathrm{d} \tilde{v}
\end{pmatrix} \\
&=
\tilde{L} (\mathrm{d} \tilde{u})^2 + 2\tilde{M} \mathrm{d} \tilde{u} \mathrm{d} \tilde{v} + \tilde{N} (\mathrm{d} \tilde{v})^2
\end{aligned}
$$

这就说明了第二基本形式$$\mathrm{II}$$与曲面$$S$$是保持定向的容许参数变换是无关的。由此可见，在有向正则曲面$$S$$上存在定义在整个曲面$$S$$上的第二基本形式$$\mathrm{II}$$，它和第一基本形式$$\mathrm{I}$$一起是有向正则曲面$$S$$上的两个基本的二次微分形式。

实际上，$$\mathrm{II} = - \mathrm{d} \boldsymbol{r} \cdot \mathrm{d} \boldsymbol{n}$$告诉我们第二基本形式可以表达为一次微分形式$$\mathrm{d} \boldsymbol{r}$$和$$\mathrm{d} \boldsymbol{n}$$内积的形式。根据一次微分形式的不变性，$$\mathrm{d} \boldsymbol{r}$$和$$\mathrm{d} \boldsymbol{n}$$在保持定向的容许参数变换下是不变的，因此第二基本形式$$\mathrm{II}$$在这样的变换下也是不变的。上面的讨论还告诉我们，若参数变换翻转曲面的定向，则$$\tilde{\boldsymbol{n}} = -\boldsymbol{n}$$，于是第二基本形式就恰好改变它的符号。

第二基本形式直接的几何意义是，它是有向距离$$\delta (\mathrm{d} u, \mathrm{d} v)$$在$$\sqrt{(\Delta u)^2 + (\Delta v)^2} \rightarrow 0$$时无穷小的主要部分的两倍，即

$$
\mathrm{II} \approx 2 \delta (\mathrm{d} u, \mathrm{d} v)
$$

### 平面的第二基本形式

**定理4.1** 一块正则曲面是平面的一部分，当且仅当它的第二基本形式恒等于零。
{:.info}

**证明** 我们首先来计算平面的第二基本形式。设$$S$$是$$\mathbb{E}^3$$中的$$Oxy$$平面，所以它的参数方程可以表示为

$$
\boldsymbol{r} = (u, v, 0)
$$

它的单位法向量为

$$
\boldsymbol{n} = (0, 0, 1)
$$

所以

$$
\begin{cases}
\begin{aligned}
\mathrm{I} &= \mathrm{d} \boldsymbol{r} \cdot \mathrm{d} \boldsymbol{r} = (\mathrm{d} u)^2 + (\mathrm{d} v)^2 \\
\mathrm{II} &= -\mathrm{d} \boldsymbol{r} \cdot \mathrm{d} \boldsymbol{n} = 0
\end{aligned}
\end{cases}
$$

因此平面的第二基本形式恒为零。接下来考虑充分性，假定正则参数曲面的参数方程是

$$
\boldsymbol{r} = \boldsymbol{r} (u, v)
$$

它的第二基本形式恒为零，即

$$
\begin{cases}
\begin{aligned}
L &= -\boldsymbol{r}_{u} \cdot n_u = 0 \\
M &= -\boldsymbol{r}_{u} \cdot n_v = -\boldsymbol{r}_{v} \cdot n_u = 0 \\
N &= -\boldsymbol{r}_{v} \cdot n_v = 0 \\
\end{aligned}
\end{cases}
$$

我们要证明它的单位法向量$$\boldsymbol{n}$$是常向量场。由于$$\boldsymbol{n}$$是单位向量场，故有

$$
\boldsymbol{n}_u \cdot \boldsymbol{n} = \boldsymbol{n}_v \cdot \boldsymbol{n} = 0
$$

注意到$$\{ \boldsymbol{r}; \boldsymbol{r}_u, \boldsymbol{r}_v, \boldsymbol{n} \}$$是空间$$\mathbb{E}^3$$中的标架，而上面的式子说明$$\boldsymbol{n}_u$$，$$\boldsymbol{n}_v$$在标架向量$$\boldsymbol{r}_u$$，$$\boldsymbol{r}_v$$，$$\boldsymbol{n}$$上的正交投影都是零，所以$$\boldsymbol{n}_u$$，$$\boldsymbol{n}_v$$都是零向量，即

$$
\mathrm{d} \boldsymbol{n} = \boldsymbol{n}_u \mathrm{d} u + \boldsymbol{n}_v \mathrm{d} v = \boldsymbol{0}
$$

因此，$$\boldsymbol{n}$$为常向量场。由于

$$
\mathrm{d} \boldsymbol{r} \cdot \boldsymbol{n} = 0
$$

所以

$$
\mathrm{d} (\boldsymbol{r} \cdot \boldsymbol{n}) = \mathrm{d} \boldsymbol{r} \cdot \boldsymbol{n} + \boldsymbol{r} \cdot \mathrm{d} \boldsymbol{n} = 0
$$

因此，$$\boldsymbol{r} \cdot \boldsymbol{n}$$为常数。于是

$$
\boldsymbol{r} (u, v) \cdot \boldsymbol{n} = \boldsymbol{r} (u_0, v_0) \cdot \boldsymbol{n}
$$

$$
\big( \boldsymbol{r} (u, v) - \boldsymbol{r} (u_0, v_0) \big) \cdot \boldsymbol{n} = 0
$$

这说明曲面$$S$$落在经过点$$\boldsymbol{r} (u_0, v_0)$$，以$$\boldsymbol{n}$$为法向量的平面内。证毕∎

### 球面的第二基本形式

**定理4.2** 一块正则曲面是球面的一部分，当且仅当在曲面上的每一点，它的第二基本形式是第一基本形式的非零倍数。
{:.info}
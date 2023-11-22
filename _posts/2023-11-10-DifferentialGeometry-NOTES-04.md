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

**证明** 设曲面$$S: \boldsymbol{r} = \boldsymbol{r} (u, v)$$是落在以$$\boldsymbol{r}_0$$为中心、以常数$$R$$为半径的球面上，则曲面的参数方程满足条件

$$
\big( \boldsymbol{r}(u, v) - \boldsymbol{r}_0 \big)^2 = R^2
$$

对上式进行微分得到

$$
\mathrm{d} \boldsymbol{r} \cdot \big( \boldsymbol{r}(u, v) - \boldsymbol{r}_0 \big) = 0
$$

由此可见，$$(\boldsymbol{r}(u, v) - \boldsymbol{r}_0)$$是曲面的法向量，故

$$
\boldsymbol{n} = \frac{1}{R} \big( \boldsymbol{r}(u, v) - \boldsymbol{r}_0 \big)
$$

因此

$$
\mathrm{II} = - \mathrm{d} \boldsymbol{r} \cdot \mathrm{d} \boldsymbol{n} = -\frac{1}{R} \mathrm{d} \boldsymbol{r} \cdot \mathrm{d} \boldsymbol{r} = -\frac{1}{R} \mathrm{I}
$$

反过来，假定有处处不为零的函数$$c(u, v)$$，使得曲面的第二基本形式和第一基本形式满足关系式

$$
\mathrm{II} = c(u, v) \cdot \mathrm{I}
$$

将上面的关系式展开便得到

$$
(L - cE) (\mathrm{d} u)^2 + 2(M - cF) \mathrm{d} u \mathrm{d} v + (N - cG) (\mathrm{d} v)^2 = 0
$$

对于任意一个固定点$$(u, v)$$，上式是关于$$(\mathrm{d} u, \mathrm{d} v)$$的恒等式，因此

$$
\begin{cases}
\begin{aligned}
L(u, v) &= c(u, v) E(u, v) \\
M(u, v) &= c(u, v) F(u, v) \\
N(u, v) &= c(u, v) G(u, v) \\
\end{aligned}
\end{cases}
$$

根据第一类基本量和第二类基本量的定义，上面的方程组等价于

$$
\begin{cases}
\begin{aligned}
(\boldsymbol{n}_u + c \ \boldsymbol{r}_u) \cdot \boldsymbol{r}_u &= 0 \\
(\boldsymbol{n}_u + c \ \boldsymbol{r}_u) \cdot \boldsymbol{r}_v &= (\boldsymbol{n}_v + c \ \boldsymbol{r}_v) \cdot \boldsymbol{r}_u =  0 \\
(\boldsymbol{n}_v + c \ \boldsymbol{r}_v) \cdot \boldsymbol{r}_v &= 0 \\
\end{aligned}
\end{cases}
$$

另一方面，$$\boldsymbol{n}$$是单位法向量场，所以

$$
(\boldsymbol{n}_u + c \ \boldsymbol{r}_u) \cdot \boldsymbol{n} = (\boldsymbol{n}_v + c \ \boldsymbol{r}_v) \cdot \boldsymbol{n} = 0
$$

由于$$\{ \boldsymbol{r}; \boldsymbol{r}_u, \boldsymbol{r}_v, \boldsymbol{n} \}$$是空间$$\mathbb{E}^3$$中的标架，上面的两组式子说明向量$$\boldsymbol{n}_u + c \boldsymbol{r}_u$$，$$\boldsymbol{n}_v + c \boldsymbol{r}_v$$在标架向量$$\boldsymbol{r}_u$$，$$\boldsymbol{r}_v$$，$$\boldsymbol{n}$$上的正交投影都是零，所以$$\boldsymbol{n}_u + c \boldsymbol{r}_u$$，$$\boldsymbol{n}_v + c \boldsymbol{r}_v$$都是零向量，即

$$
\begin{cases}
\begin{aligned}
\boldsymbol{n}_u + c \boldsymbol{r}_u &= \boldsymbol{0} \\
\boldsymbol{n}_v + c \boldsymbol{r}_v &= \boldsymbol{0} \\
\end{aligned}
\end{cases}
$$

将上式分别对$$u$$，$$v$$求导得到

$$
\begin{cases}
\begin{aligned}
\boldsymbol{n}_{uv} + c_v \boldsymbol{r}_u + c \boldsymbol{r}_{uv} &= \boldsymbol{0} \\
\boldsymbol{n}_{vu} + c_u \boldsymbol{r}_v + c \boldsymbol{r}_{vu} &= \boldsymbol{0} \\
\end{aligned}
\end{cases}
$$

比较这两个式子得到

$$
c_v \boldsymbol{r}_u = c_u \boldsymbol{r}_v
$$

因为$$\boldsymbol{r}_u$$，$$\boldsymbol{r}_v$$是线性无关的，上面的式子意味着

$$
c_u = c_v = 0
$$

即$$c(u, v) = c$$是常数。因此有

$$
\mathrm{d} (\boldsymbol{n} + c \boldsymbol{r}) = (\boldsymbol{n}_u + c \boldsymbol{r}_u) \mathrm{d} u + (\boldsymbol{n}_v + c \boldsymbol{r}_v) \mathrm{d} v = \boldsymbol{0}
$$

故$$\boldsymbol{n} + c \boldsymbol{r}$$是定义在曲面$$S$$上的常向量场。不妨设有常向量$$\boldsymbol{r}_0$$使得

$$
\boldsymbol{n} + c \boldsymbol{r} = c \boldsymbol{r}_0
$$

于是

$$
\boldsymbol{r} (u, v) - \boldsymbol{r}_0 = -\frac{1}{c} \boldsymbol{n} (u,v)
$$

$$
\big( \boldsymbol{r} (u, v) - \boldsymbol{r}_0 \big)^2 = \frac{1}{c^2}
$$

即曲面$$S$$落在以$$\boldsymbol{r}_0$$为中心、以$$\frac{1}{\vert c \vert}$$为半径的球面上。证毕∎

定理4.2的条件的意义是在曲面上的每一点，曲面沿各个方向的弯曲程度都是相同的。这个条件用下一节要介绍的法曲率的概念来表达将会变得更加清晰。定理4.2结论是很强的，它的意思是：如果曲面上在每一个固定点沿各个方向的弯曲程度都是相同的，则它在各个点、沿各个方向的弯曲程度都是相同的。

## 法曲率

设曲面$$S$$的参数方程是$$\boldsymbol{r} = \boldsymbol{r} (u, v)$$，它上面的曲线$$C$$可以用参数方程

$$
\begin{cases}
\begin{aligned}
u &= u(s) \\ v &= v(s)
\end{aligned}
\end{cases}
$$

来表示，假定这里的$$s$$是曲线的弧长参数。作为空间$$\mathbb{E}^3$$中的曲线，$$C$$的参数方程将是

$$
\boldsymbol{r} = \boldsymbol{r} (u(s), v(s))
$$

因此它的单位切向量是

$$
\boldsymbol{\alpha} (s) = \frac{\mathrm{d} \boldsymbol{r}}{\mathrm{d} s} = \boldsymbol{r}_u \frac{\mathrm{d} u(s)}{\mathrm{d} s} + \boldsymbol{r}_v \frac{\mathrm{d} v(s)}{\mathrm{d} s}
$$

曲率向量是

$$
\begin{aligned}
\frac{\mathrm{d} \boldsymbol{\alpha}}{\mathrm{d} s} &= \kappa \boldsymbol{\beta} \\
&= \boldsymbol{r}_{uu} \bigg( \frac{\mathrm{d} u(s)}{\mathrm{d} s} \bigg)^2 + 2 \boldsymbol{r}_{uv} \frac{\mathrm{d} u(s)}{\mathrm{d} s} \frac{\mathrm{d} v(s)}{\mathrm{d} s} + \boldsymbol{r}_{vv} \bigg( \frac{\mathrm{d} v(s)}{\mathrm{d} s} \bigg)^2 \\
&+ \boldsymbol{r}_u \frac{\mathrm{d}^2 u(s)}{\mathrm{d} s^2} + \boldsymbol{r}_v \frac{\mathrm{d}^2 v(s)}{\mathrm{d} s^2}
\end{aligned}
$$

因此曲线$$C$$的曲率向量在曲面的法向量$$\boldsymbol{n}$$上的正交投影是

$$
\begin{aligned}
\kappa_n &= \frac{\mathrm{d} \boldsymbol{\alpha}}{\mathrm{d} s} \cdot \boldsymbol{n} = \kappa (\boldsymbol{\beta} \cdot \boldsymbol{n}) \\
&= L \bigg( \frac{\mathrm{d} u(s)}{\mathrm{d} s} \bigg)^2 + 2M \frac{\mathrm{d} u(s)}{\mathrm{d} s} \frac{\mathrm{d} v(s)}{\mathrm{d} s}  + N \bigg( \frac{\mathrm{d} v(s)}{\mathrm{d} s} \bigg)^2
\end{aligned}
$$

从上面的表达式可以知道，$$\kappa_n$$只依赖于曲面在该点的第二类基本量$$L$$、$$M$$、$$N$$，以及曲线$$C$$的单位切向量$$\big( \frac{\mathrm{d} u(s)}{\mathrm{d} s}, \frac{\mathrm{d} v(s)}{\mathrm{d} s} \big)$$，通常把$$\kappa_n$$称为曲面$$S$$上曲线$$C$$的**法曲率**。由此可见，如果曲面$$S$$上由两条曲线$$C_1$$，$$C_2$$在$$p$$处有相同的单位切向量，则这两条曲线在点$$p$$有相同的法曲率。这个结论也称为[梅尼埃定理](https://en.wikipedia.org/wiki/Meusnier%27s_theorem)。

命$$\angle (\boldsymbol{\beta}, \boldsymbol{n}) = \theta$$是曲线$$C$$的主法向量$$\boldsymbol{\beta}$$与曲面$$S$$的法向量$$\boldsymbol{n}$$之间的夹角，则有

$$
\kappa_n = \kappa \cos{\theta}
$$

从上式还能得到一个有趣的事实：在曲面$$S$$上考虑经过点$$p = \boldsymbol{r} (u(s), v(s))$$，并且在点$$p$$处彼此相切的所有曲线，则这些曲线在点$$p$$的[曲率中心](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲率圆)都落在与该切方向垂直的平面(这些曲线的公共的法平面)内直径为$$\frac{1}{\vert \kappa_n \vert}$$的圆周上，如下图所示。

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/vkrfZFs.png" width="80%">
</div>

根据关系式$$\frac{1}{\kappa} = \frac{1}{\kappa_n} \cos \theta$$，可以得到曲线$$C$$的曲率中心是

$$
\begin{aligned}
\boldsymbol{c} &= \boldsymbol{r} (u(s), v(s)) + \frac{1}{\kappa} \boldsymbol{\beta} \\
&= \boldsymbol{r} (u(s), v(s)) + \frac{1}{\vert \kappa_n \vert} \cos \theta \cdot \boldsymbol{\beta}
\end{aligned}
$$

所以

$$
\vert \boldsymbol{c} - \boldsymbol{r} (u(s), v(s)) \vert^2 = \frac{1}{\kappa_n^2} \cos^2 \theta
$$

由于曲面上在一点相切的曲线在该点有相同的法曲率，所以法曲率的概念可以抽象出来作为曲面上在一点的切方向的函数。事实上，因为$$s$$是曲线$$\boldsymbol{r} (s) = \boldsymbol{r} (u(s), v(s))$$的弧长参数，所以

$$
\vert \boldsymbol{r}'(s) \vert^2 = E \bigg( \frac{\mathrm{d} u(s)}{\mathrm{d} s} \bigg)^2 + 2F \frac{\mathrm{d} u(s)}{\mathrm{d} s} \frac{\mathrm{d} v(s)}{\mathrm{d} s} + G \bigg( \frac{\mathrm{d} v(s)}{\mathrm{d} s} \bigg)^2 = 1
$$

即

$$
(\mathrm{d} s)^2 = E (\mathrm{d} u)^2 + 2F \mathrm{d} u \mathrm{d} v + G (\mathrm{d} v)^2 = \mathrm{I}
$$

带入法曲率$$\kappa_n$$得到

$$
\kappa_n = \frac{L (\mathrm{d} u)^2 + 2M \mathrm{d} u \mathrm{d} v + N (\mathrm{d} v)^2}{(\mathrm{d} s)^2} = \frac{\mathrm{II}}{\mathrm{I}}
$$

上述表达式的分子和分母都是$$(\mathrm{d} u, \mathrm{d} u)$$的二次齐次多项式，因此它只是$$\frac{\mathrm{d} u}{\mathrm{d} v}$$的函数。

**定义4.1** 设正则参数曲面$$S$$的参数方程是$$\boldsymbol{r} = \boldsymbol{r} (u, v)$$，$$\mathrm{I}$$和$$\mathrm{II}$$分别是它的第一基本形式和第二基本形式，则
$$
\kappa_n = \frac{\mathrm{II}}{\mathrm{I}} = \frac{L (\mathrm{d} u)^2 + 2M \mathrm{d} u \mathrm{d} v + N (\mathrm{d} v)^2}{E (\mathrm{d} u)^2 + 2F \mathrm{d} u \mathrm{d} v + G (\mathrm{d} v)^2}
$$
称为曲面$$S$$在点$$(u, v)$$沿切方向$$(\mathrm{d} u, \mathrm{d} v)$$的**法曲率**。
{:.success}

### 法截面和法截线

因此，曲面$$S$$在点$$(u, v)$$处沿切方向$$(\mathrm{d} u, \mathrm{d} v)$$的法曲率恰好等于曲面$$S$$上经过点$$(u, v)$$、以$$(\mathrm{d} u, \mathrm{d} v)$$为切方向的曲线在该点的法曲率。曲面$$S$$在点$$(u, v)$$处由切方向$$(\mathrm{d} u, \mathrm{d} v)$$和法向量$$\boldsymbol{n} (u, v)$$决定了一个平面，称为曲面$$S$$在该点处由切方向$$(\mathrm{d} u, \mathrm{d} v)$$确定的**法截面**。法截面与曲面$$S$$本身相交成一条平面曲线，它是曲面$$S$$上经过点$$(u, v)$$、以$$(\mathrm{d} u, \mathrm{d} v)$$为切方向的一条曲线，称为曲面在该点的一条**法截线**。

根据前面的讨论，曲面$$S$$上所有在点$$(u, v)$$处与法截线相切的曲线在该点有相同的法曲率，也就是法截线在该点处的法曲率。由于法截线是曲面$$S$$上经过点$$(u, v)$$、以$$(\mathrm{d} u, \mathrm{d} v)$$为切方向的平面曲线，它以曲面在该点的法向量$$\boldsymbol{n}$$为法向量，也就是它的主法向量$$\boldsymbol{\beta} = \pm \boldsymbol{n}$$，因此有

$$
\kappa = \vert \kappa_n \vert
$$

如果规定曲面$$S$$在点$$(u, v)$$处由切方向$$(\mathrm{d} u, \mathrm{d} v)$$确定的法截面以切方向$$(\mathrm{d} u, \mathrm{d} v)$$到曲面的法向量$$\boldsymbol{n} (u, v)$$的旋转方向为正定向，那么上面的结果还可以更准确的描述为

**定理4.3** 曲面$$S$$在点$$(u, v)$$处沿切方向$$(\mathrm{d} u, \mathrm{d} v)$$的法曲率$$\kappa_n$$，等于以曲面$$S$$在该点处由切方向$$(\mathrm{d} u, \mathrm{d} v)$$确定的法截线作为相应的有向法截面上的平面曲线的相对曲率$$\kappa_r$$。
{:.info}

在直观上，可以把法截面想象为与曲面在一点处垂直(即包含曲面在该点的法线)的"刀"，法截线就是用这把刀在曲面上切割出来的剖面线。法曲率恰好是曲面在该点沿相应的切方向的剖面线的相对曲率。

### Euler公式

假定曲面$$S: \boldsymbol{r} = \boldsymbol{r} (u, v)$$的参数系$$(u, v)$$在点$$\boldsymbol{r} (u_0, v_0)$$处是正交的，于是曲面$$S$$在该点的第一基本形式和第二基本形式分别是

$$
\begin{cases}
\begin{aligned}
\mathrm{I} &= E (\mathrm{d} u)^2 + G (\mathrm{d} v)^2 \\
\mathrm{II} &= L (\mathrm{d} u)^2 + 2M \mathrm{d} u \mathrm{d} v + G (\mathrm{d} v)^2 \\
\end{aligned}
\end{cases}
$$

所以曲面$$S$$在该点的法曲率是

$$
\begin{aligned}
\kappa_n &= \frac{\mathrm{II}}{\mathrm{I}} = \frac{L (\mathrm{d} u)^2 + 2M \mathrm{d} u \mathrm{d} v + G (\mathrm{d} v)^2}{E (\mathrm{d} u)^2 + G (\mathrm{d} v)^2} \\
&= \frac{L}{E} \bigg( \frac{\sqrt{E} \mathrm{d} u}{\sqrt{E (\mathrm{d} u)^2 + G (\mathrm{d} v)^2}} \bigg)^2 \\
&+ \frac{2M}{\sqrt{EG}} \frac{\sqrt{E} \mathrm{d} u}{\sqrt{E (\mathrm{d} u)^2 + G (\mathrm{d} v)^2}} \frac{\sqrt{G} \mathrm{d} v}{\sqrt{E (\mathrm{d} u)^2 + G (\mathrm{d} v)^2}} \\
&+ \frac{N}{G} \bigg( \frac{\sqrt{G} \mathrm{d} v}{\sqrt{E (\mathrm{d} u)^2 + G (\mathrm{d} v)^2}} \bigg)^2
\end{aligned}
$$

用$$\theta$$记切方向$$(\mathrm{d}u, \mathrm{d}v)$$与$$u$$-曲线切方向的夹角，则

$$
\begin{cases}
\begin{aligned}
\cos{\theta} &= \frac{\sqrt{E} \mathrm{d} u}{\sqrt{E (\mathrm{d} u)^2 + G (\mathrm{d} v)^2}} \\
\sin{\theta} &= \frac{\sqrt{G} \mathrm{d} v}{\sqrt{E (\mathrm{d} u)^2 + G (\mathrm{d} v)^2}} \\
\end{aligned}
\end{cases}
$$

因此

$$
\begin{aligned}
\kappa_n (\theta) &= \frac{L}{E} \cos^2{\theta} + \frac{2M}{\sqrt{EG}} \cos{\theta} \sin{\theta} + \frac{N}{G} \sin^2{\theta} \\
&= \frac{L}{E} \frac{1 + \cos{2 \theta}}{2} + \frac{M}{\sqrt{EG}} \sin{2 \theta} + \frac{N}{G} \frac{1 - \cos{2 \theta}}{2} \\
&= \frac{1}{2} \bigg( \frac{L}{E} + \frac{N}{G} \bigg) + \frac{1}{2} \bigg( \frac{L}{E} - \frac{N}{G} \bigg) \cos{2 \theta} + \frac{M}{\sqrt{EG}} \sin{2 \theta}
\end{aligned}
$$

命

$$
A = \sqrt{\bigg( \frac{1}{2} \bigg( \frac{L}{E} - \frac{N}{G} \bigg) \bigg)^2 + \bigg( \frac{M}{\sqrt{EG}} \bigg)^2}
$$

则当$$A \neq 0$$是可以引入辅助角$$\theta_0$$使得

$$
\begin{cases}
\begin{aligned}
\cos{2 \theta_0} &= \frac{1}{2A} \bigg( \frac{L}{E} - \frac{N}{G} \bigg) \\
\sin{2 \theta_0} &= \frac{M}{A \sqrt{EG}} \\
\end{aligned}
\end{cases}
$$

于是

$$
\begin{aligned}
\kappa_n (\theta) &= \frac{1}{2} \bigg( \frac{L}{E} + \frac{N}{G} \bigg) + A (\cos{2 \theta} \cos{2 \theta_0} + \sin{2 \theta} \sin{2 \theta_0}) \\
&= \frac{1}{2} \bigg( \frac{L}{E} + \frac{N}{G} \bigg) + A \cos{2(\theta - \theta_0)}
\end{aligned}
$$

由此可见，当$$\theta = \theta_0$$时，法曲率$$\kappa_n (\theta)$$取最大值

$$
\kappa_1 = \frac{1}{2} \bigg( \frac{L}{E} + \frac{N}{G} \bigg) + \sqrt{\bigg( \frac{1}{2} \bigg( \frac{L}{E} - \frac{N}{G} \bigg) \bigg)^2 + \bigg( \frac{M}{\sqrt{EG}} \bigg)^2}
$$

当$$\theta = \theta_0 + \frac{\pi}{2}$$时，法曲率$$\kappa_n (\theta)$$取最小值

$$
\kappa_2 = \frac{1}{2} \bigg( \frac{L}{E} + \frac{N}{G} \bigg) - \sqrt{\bigg( \frac{1}{2} \bigg( \frac{L}{E} - \frac{N}{G} \bigg) \bigg)^2 + \bigg( \frac{M}{\sqrt{EG}} \bigg)^2}
$$

而当$$A = 0$$时，法曲率$$\kappa_n (\theta)$$与角$$\theta$$无关，即

$$
\kappa_n (\theta) = \frac{1}{2} \bigg( \frac{L}{E} + \frac{N}{G} \bigg)
$$

无论如何，上面的结果可以叙述成下列定理：

**定理4.4** 正则参数曲面在任意一个固定点，其法曲率必定在两个彼此正交的切方向上分别取最大值和最小值。
{:.info}

**定义4.2** 正则参数曲面在任意一个固定点，其法曲率取最大值和最小值的方向称为曲面在该点的**主方向**，相应的法曲率称为曲面在该点的**主曲率**。
{:.success}

根据法曲率$$\kappa_n (\theta)$$的表达式，沿方向角为$$\theta$$的切方向的法曲率可以由两个主曲率来表示

$$
\kappa_n (\theta) = \kappa_1 \cos^2{(\theta - \theta_0)} + \kappa_2 \sin^2{(\theta - \theta_0)}
$$

上式也称为法曲率的**Euler公式**。

### 渐近方向和渐近曲线

**定义4.3** 在曲面$$S$$上一点，其法曲率为零的切方向称为曲面$$S$$在该点的**渐近方向**。如果曲面$$S$$上一条曲线在每一点的切方向都是曲面在该点的渐近方向，则称该曲线是曲面$$S$$上的**渐近曲线**。
{:.success}

在一个固定点$$(u, v)$$，渐近方向$$(\mathrm{d} u, \mathrm{d} v)$$是二次方程

$$
L (\mathrm{d} u)^2 + 2M \mathrm{d} u \mathrm{d} v + G (\mathrm{d} v)^2 = 0
$$

的解。因此，曲面在点$$(u, v)$$有实渐近方向的充分必要条件是

$$
LN - M^2 \leq 0
$$

当$$LN - M^2 \lt 0$$时有两个不同的实渐近方向，它们是

$$
\frac{\mathrm{d} u}{\mathrm{d} v} = \frac{-M \pm \sqrt{M^2 - LN}}{L} = \frac{N}{-M \mp \sqrt{M^2 - LN}}
$$

当$$LN - M^2 = 0$$时有一个实渐近方向(或者认为两个实渐近方向重合在一起)，它是

$$
\frac{\mathrm{d} u}{\mathrm{d} v} = -\frac{M}{L} = -\frac{N}{M}
$$

把$$(u, v)$$看作动点则二次方程$$L (\mathrm{d} u)^2 + 2M \mathrm{d} u \mathrm{d} v + G (\mathrm{d} v)^2 = 0$$是渐近曲线的微分方程。特别是，如果曲面上条件$$LN - M^2 \lt 0$$处处成立，则在曲面上存在两个处处线性无关的渐近方向场。于是根据[定理3.2](/2023/10/18/DifferentialGeometry-NOTES-03.html#曲面上正交参数曲线网的存在性)，在曲面上存在由渐近曲线构成的参数曲线网。

**定理4.5** 曲面上的参数曲线网是渐近曲线网的充分必要条件是$$L = N = 0$$。
{:.info}

**证明** 如果曲面上的参数曲线网是渐近曲线网，即$$u$$-曲线和$$v$$-曲线都是渐近曲线，于是$$(\mathrm{d} u, \mathrm{d} v) = (1, 0)$$和$$(\mathrm{d} u, \mathrm{d} v) = (0, 1)$$都是渐近方向。将它们分别带入二次方程$$L (\mathrm{d} u)^2 + 2M \mathrm{d} u \mathrm{d} v + G (\mathrm{d} v)^2 = 0$$便得到$$L = N = 0$$。

反过来，如果$$L = N = 0$$，则二次方程成为

$$
2M \mathrm{d} u \mathrm{d} v = 0
$$

它的解是$$\mathrm{d} u = 0$$和$$\mathrm{d} v = 0$$，即$$u$$-曲线和$$v$$-曲线都是渐近曲线。证毕∎

**定理4.6** 曲面上的一条曲线是渐近曲线，当且仅当或者它是一条直线，或者它的密切平面恰好是曲面的切平面。
{:.info}

**证明** 根据法曲率公式

$$
\kappa_n = \kappa \cos{\theta}
$$

其中$$\theta$$是曲线的主法向量$$\boldsymbol{\beta}$$与曲面的法向量$$\boldsymbol{n}$$之间的夹角。因此，$$\kappa_n = 0$$的充分必要条件是$$\kappa = 0$$或者$$\cos{\theta} = 0$$。如果处处有$$\kappa = 0$$，则该曲线是直线。如果在曲线上有一点使$$\kappa \neq 0$$，则必定有$$\cos{\theta} = 0$$，故$$\theta = \frac{\pi}{2}$$，于是$$\boldsymbol{\beta}$$与曲面的法向量$$\boldsymbol{n}$$垂直，即曲线的密切平面与曲面相切。证毕∎

## Weingarten映射和主曲率

### Gauss映射

设$$\boldsymbol{r} = \boldsymbol{r} (u,v)$$是一块正则参数曲面，它在每一点处有一个确定的单位法向量$$\boldsymbol{n} (u, v)$$。将$$\boldsymbol{n} (u, v)$$在$$\mathbb{E}^3$$中平行移动到坐标原点$$O$$，那么它的终点便落在$$\mathbb{E}^3$$中的单位球面$$\Sigma$$上，于是得到从曲面$$S$$到$$\Sigma$$的一个可微映射$$g: S \rightarrow \Sigma$$使得

$$
g (\boldsymbol{r} (u, v)) = \boldsymbol{n} (u, v)
$$

这个映射称为**Gauss映射**。很明显，当曲面$$S$$弯曲得比较厉害时， 则当曲面$$S$$上的点变动时其相应的法向量的变化就比较大，于是法向量场在$$\Sigma$$上所扫过的面积与曲面上的点扫过的面积之比就比较大，如下图所示。这正是Gauss观察曲面形状的出发点。据说，Gauss的灵感来自他担任天文台台长时从事大地测量的研究工作。

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/WR2A38L.png" width="80%">
</div>

### Weingarten映射

在[正则参数曲面之间的对应](/2023/10/18/DifferentialGeometry-NOTES-03.html#正则参数曲面之间的对应)一节我们提到过两个曲面之间的可微映射在对应点的切空间之间诱导出一个线性映射，称为该映射的切映射。这样，Gauss映射$$g: S \rightarrow \Sigma$$便诱导出从曲面$$S$$在点$$p$$的切空间$$T_p S$$到球面$$\Sigma$$在像点$$g(p)$$的切空间$$T_{g(p)} \Sigma$$的切映射

$$
g_* : T_p S \rightarrow T_{g(p)} \Sigma
$$

下面我们来求这个切映射的表达式：

设曲面$$S$$上的一条曲线的参数方程是

$$
\begin{cases}
\begin{aligned}
u &= u(t) \\ v &= v(t)
\end{aligned}
\end{cases}
$$

于是它在Gauss映射下的像是

$$
g (\boldsymbol{r} (u(t), v(t))) = \boldsymbol{n} (u(t), v(t))
$$

根据诱导切映射的定义

$$
g_* \bigg( \frac{\mathrm{d} \boldsymbol{r}}{\mathrm{d} t} \bigg) = \frac{\mathrm{d} \boldsymbol{n} (u(t), v(t))}{\mathrm{d} t} = \boldsymbol{n}_u \frac{\mathrm{d} u(t)}{\mathrm{d} t} + \boldsymbol{n}_v \frac{\mathrm{d} v(t)}{\mathrm{d} t}
$$

因此

$$
\begin{cases}
\begin{aligned}
g_* (\boldsymbol{r}_u) &= \boldsymbol{n}_u \\ 
g_* (\boldsymbol{r}_v) &= \boldsymbol{n}_v
\end{aligned}
\end{cases}
$$

由于$$\boldsymbol{n}$$是球面$$\Sigma$$的向径，因此它本身也是球面$$\Sigma$$的法向量，这就是说曲面$$S$$在点$$p$$的切平面和球面$$\Sigma$$在点$$g(p)$$的切平面是彼此平行的，特别是切空间$$T_p S$$和切空间$$T_{g(p)} \Sigma$$可以自然地等同起来，于是球面$$\Sigma$$的切向量$$\boldsymbol{n}_u$$、$$\boldsymbol{n}_v$$可以看作曲面$$S$$的切向量。这样，切映射$$g_*$$成为从切空间$$T_p S$$到它自身的线性映射。命

$$
W = -g_* : T_p S \rightarrow T_{p} S
$$

称$$W$$为曲面$$S$$在点$$p$$的**Weingarten映射**。据线性代数的理论，在具有欧氏内积的向量空间上的自共轭线性变换和二次型是彼此确定的。我们这里定义的Weingarten映射和曲面的第二基本形式恰好有这种关系。

**定理4.7** 曲面$$S$$的第二基本形式$$\mathrm{II}$$可以用Weingarten映射表示成
$$\mathrm{II} = W(\mathrm{d} \boldsymbol{r}) \cdot \mathrm{d} \boldsymbol{r}$$
。
{:.info}

**证明** 曲面$$S$$上任意一个切向量可以表示成

$$
\mathrm{d} \boldsymbol{r} = \boldsymbol{r}_u \mathrm{d} u + \boldsymbol{r}_v \mathrm{d} v
$$

其中$$\mathrm{d} u$$、$$\mathrm{d} v$$是切向量的分量。利用Weingarten映射的定义有

$$
\begin{aligned}
W(\mathrm{d} \boldsymbol{r}) &= W (\boldsymbol{r}_u \mathrm{d} u + \boldsymbol{r}_v \mathrm{d} v) = -g_* (\boldsymbol{r}_u \mathrm{d} u + \boldsymbol{r}_v \mathrm{d} v) \\
&= -g_* (\boldsymbol{r}_u) \mathrm{d} u - g_* (\boldsymbol{r}_v) \mathrm{d} v \\
&= -(\boldsymbol{n}_u \mathrm{d} u + \boldsymbol{n}_v \mathrm{d} v) \\
&= - \mathrm{d} n
\end{aligned}
$$

所以

$$
\mathrm{II} = - \mathrm{d} n \cdot \mathrm{d} \boldsymbol{r} = W(\mathrm{d} \boldsymbol{r}) \cdot \mathrm{d} \boldsymbol{r}
$$

证毕∎

**定理4.8** Weingarten映射$$W$$是从切空间$$T_p S$$到它自身的共轭映射，即对于曲面$$S$$在点$$(u, v)$$的任意两个切方向$$\mathrm{d} \boldsymbol{r}$$和$$\delta \boldsymbol{r}$$满足
$$
W(\mathrm{d} \boldsymbol{r}) \cdot \delta \boldsymbol{r} = \mathrm{d} \boldsymbol{r} \cdot W(\delta \boldsymbol{r})
$$
。
{:.info}

**证明** 设

$$
\begin{cases}
\begin{aligned}
\mathrm{d} \boldsymbol{r} &= \boldsymbol{r}_u \mathrm{d} u + \boldsymbol{r}_v \mathrm{d} v \\
\delta \boldsymbol{r} &= \boldsymbol{r}_u \delta u + \boldsymbol{r}_v \delta v \\
\end{aligned}
\end{cases}
$$

利用Weingarten映射的定义有

$$
\begin{cases}
\begin{aligned}
W(\mathrm{d} \boldsymbol{r}) &= - (\boldsymbol{n}_u \mathrm{d} u + \boldsymbol{n}_v \mathrm{d} v)\\
W(\delta \boldsymbol{r}) &= - (\boldsymbol{n}_u \delta u + \boldsymbol{n}_v \delta v)
\end{aligned}
\end{cases}
$$

这样

$$
\begin{aligned}
W(\mathrm{d} \boldsymbol{r}) \cdot \delta \boldsymbol{r} &= -(\boldsymbol{n}_u \mathrm{d} u + \boldsymbol{n}_v \mathrm{d} v) \cdot (\boldsymbol{r}_u \delta u + \boldsymbol{r}_v \delta v ) \\
&= L \mathrm{d} u \delta u + M (\mathrm{d} u \delta v + \mathrm{d} v \delta u) + N \mathrm{d} v \delta u \\
&= -(\boldsymbol{r}_u \mathrm{d} u + \boldsymbol{r}_v \mathrm{d} v) \cdot (\boldsymbol{n}_u \delta u + \boldsymbol{n}_v \delta v) \\
&= \mathrm{d} \boldsymbol{r} \cdot W(\delta \boldsymbol{r})
\end{aligned}
$$

证毕∎

## 主方向和主曲率的计算

## Dupin标形和曲面参数方程在一点的标准展开

## 某些特殊曲面
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
\mathrm{d} s^2 = E (\mathrm{d} u)^2 + 2F \mathrm{d} u \mathrm{d} v + G (\mathrm{d} v)^2 = \mathrm{I}
$$

带入法曲率$$\kappa_n$$得到

$$
\kappa_n = \frac{L (\mathrm{d} u)^2 + 2M \mathrm{d} u \mathrm{d} v + N (\mathrm{d} v)^2}{\mathrm{d} s^2} = \frac{\mathrm{II}}{\mathrm{I}}
$$

上述表达式的分子和分母都是$$(\mathrm{d} u, \mathrm{d} u)$$的二次齐次多项式，因此它只是$$\frac{\mathrm{d} u}{\mathrm{d} v}$$的函数。

**定义4.1** 设正则参数曲面$$S$$的参数方程是$$\boldsymbol{r} = \boldsymbol{r} (u, v)$$，$$\mathrm{I}$$和$$\mathrm{II}$$分别是它的第一基本形式和第二基本形式，则
$$
\kappa_n = \frac{\mathrm{II}}{\mathrm{I}} = \frac{L (\mathrm{d} u)^2 + 2M \mathrm{d} u \mathrm{d} v + N (\mathrm{d} v)^2}{E (\mathrm{d} u)^2 + 2F \mathrm{d} u \mathrm{d} v + G (\mathrm{d} v)^2}
$$
称为曲面$$S$$在点$$(u, v)$$沿切方向$$(\mathrm{d} u, \mathrm{d} v)$$的**法曲率**。
{:.success}

## Weingarten映射和主曲率

## 主方向和主曲率的计算

## Dupin标形和曲面参数方程在一点的标准展开

## 某些特殊曲面
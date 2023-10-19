---
layout: article
title: 微分几何笔记03-曲面的第一基本形式
tags: ["CG", "Geometry Processing", "Math", "Differential Geometry"]
key: DifferentialGeometry-03
aside:
  toc: true
sidebar:
  nav: DifferentialGeometry
---

> 这个系列是北京大学陈维桓教授《微分几何(第二版)》的学习笔记，主要涉及古典微分几何中曲线曲面理论的相关知识。系统学习微分几何对于理解计算机图形学中的各种几何处理算法是十分有益的。本节介绍曲面的第一基本形式。
<!--more-->

## 正则参数曲面

所谓的参数曲面$$S$$是指从$$\mathbb{E}^2$$的一个区域$$D$$(即$$\mathbb{E}^2$$中的一个连通开子集)到空间$$\mathbb{E}^3$$的一个连续映射$$S: D \rightarrow \mathbb{E}^3$$。若在$$\mathbb{E}^2$$和$$\mathbb{E}^3$$中分别建立了笛卡儿直角坐标系，则参数曲面$$S$$的方程可以表示为：

$$
\begin{cases}
x = x(u, v) \\
y = y(u, v) \\
z = z(u, v) \\
\end{cases}
\ \ \ \ (u, v) \in D
$$

或者写成向量方程的形式：

$$
\boldsymbol{r} = \boldsymbol{r} (u, v) = \big( x(u, v), y(u, v), z(u, v) \big)
$$

自变量$$u$$和$$v$$称为曲面$$S$$的参数。在曲面$$S$$上取一点$$p_0$$，$$\overrightarrow{Op_0} = \boldsymbol{r} (u_0, v_0)$$。如果让参数$$u$$固定$$u = u_0$$，而让参数$$v$$变化，则动点描出一条落在曲面$$S$$上的曲线$$\boldsymbol{r} (u_0, v)$$，这条曲线称为在曲面$$S$$上经过点$$p_0$$的$$v$$-曲线。同理，我们有曲面$$S$$上经过点$$p_0$$的$$u$$-曲线$$\boldsymbol{r} (u, v_0)$$，或记成$$v = v_0$$。这样，在参数曲面上经过每一点有一条$$u$$-曲线和一条$$v$$-曲线，它们构成曲面上的**参数曲线网**。在区域$$D$$上看，$$u$$-曲线和$$v$$-曲线分别是$$\mathbb{E}^2$$中的坐标曲线。因此在直观上，参数曲面$$S$$是把$$\mathbb{E}^2$$中的区域$$D$$映射到$$\mathbb{E}^3$$中的结果，此时$$\mathbb{E}^2$$中的坐标曲线网就变成了曲面$$S$$中的参数曲线网。这就是说，从曲面$$S$$上看，$$(u, v)$$可以作为曲面$$S$$上点的坐标，称为曲面上的**曲纹坐标**。

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/149o2Eg.png" width="80%">
</div>

但是，要使$$(u, v)$$真的能够具有曲面$$S$$上点的坐标的功能，必须要求在曲面$$S$$和区域$$D$$的点之间是一一对应的，显然上面提到的方程组本身并不能满足这一点。为此，需要在方程上加一些正则性条件。曲面$$S$$的参数曲线在点$$p_0$$的两个切向量是

$$
\boldsymbol{r}_u (u_0, v_0) = \frac{\partial \boldsymbol{r}}{\partial u} \bigg|_{(u_0, v_0)} \ \
\boldsymbol{r}_v (u_0, v_0) = \frac{\partial \boldsymbol{r}}{\partial v} \bigg|_{(u_0, v_0)}
$$

如果$$\boldsymbol{r}_u (u_0, v_0)$$和$$\boldsymbol{r}_v (u_0, v_0)$$是线性无关的，即$$\boldsymbol{r}_u \times \boldsymbol{r}_v \neq \mathbf{0}$$，则称曲面$$S$$在点$$p_0$$是**正则**的。今后我们所研究的曲面都是3次以上连续可微的、处处是正则点的参数曲面，称为**正则参数曲面**。

### Monge形式

设$$S: \boldsymbol{r} = \boldsymbol{r}(u, v)$$是正则参数曲面，对于任一点$$(u_0, v_0) \in D$$有

$$
\boldsymbol{r}_u \times \boldsymbol{r}_v \vert_{(u_0, v_0)} = 
\bigg( \frac{\partial (y, z)}{\partial (u, v)}, \frac{\partial (z, x)}{\partial (u, v)}, \frac{\partial (x, y)}{\partial (u, v)} \bigg) \bigg|_{(u_0, v_0)} \neq \mathbf{0}
$$

不妨设

$$
\frac{\partial (x, y)}{\partial (u, v)} \bigg|_{(u_0, v_0)} \neq 0
$$

故由反函数定理得知，存在点$$(u_0, v_0)$$在$$D$$内的邻域$$U$$，使得函数$$x=x(u, v)$$，$$y=y(u, v)$$在$$U$$上有反函数

$$
\begin{cases}
u = u(x, y) \\
v = v(x, y)
\end{cases}
$$

即它们满足恒等式

$$
\begin{cases}
x\big( u(x, y), v(x, y) \big) \equiv x \\ 
y\big( u(x, y), v(x, y) \big) \equiv y \\ 
\end{cases}
$$

这时

$$
z = z(u, v) = z(u(x, y), v(x, y))
$$

将上式右端仍旧记为函数$$z(x, y)$$，则曲面$$S$$的参数方程成为：

$$
\boldsymbol{r} = (x, y, z(x, y))
$$

于是区域$$U$$与曲面$$S\vert_U$$之间的点的一一对应是由$$(u(x, y), v(x, y)) \rightarrow (x, y, z(x, y))$$给出的。

上面的讨论还说明，正则参数曲面在任意一点的某个邻域内总是可以表示成类似于$$z = z(x, y)$$的形式。也就是说，正则参数曲面在局部上必定可以看作一个二元连续可微函数的图像。用$$z = z(x, y)$$给出曲面的方式称为**Monge形式**。对于Monge形式给出的曲面，其参数方程恰好是$$\boldsymbol{r} = (x, y, z(x, y))$$。因此有

$$
\boldsymbol{r}_x = (1, 0, z_x), \ \
\boldsymbol{r}_y = (0, 1, z_y)
$$

于是

$$
\boldsymbol{r}_x \times \boldsymbol{r}_y = \bigg( -\frac{\partial z}{\partial x}, -\frac{\partial z}{\partial y}, 1 \bigg) \neq \mathbb{0}
$$

即Monge形式给出的曲面都是正则的。

### 参数变换

正则参数曲面的参数容许作一定的变换。设

$$
\begin{cases}
u = u(\tilde{u}, \tilde{v}) \\
v = v(\tilde{u}, \tilde{v}) \\
\end{cases}
$$

它们满足如下的条件：

(1) $$u(\tilde{u}, \tilde{v})$$、$$v(\tilde{u}, \tilde{v})$$都是$$\tilde{u}$$、$$\tilde{v}$$的3次以上连续可微函数；

(2) $$\frac{\partial (u, v)}{\partial (\tilde{u}, \tilde{v})} \neq 0$$

将上面的函数代入正则参数曲面的方程可以得到

$$
\begin{aligned}
\boldsymbol{r} &= \boldsymbol{r} (u(\tilde{u}, \tilde{v}), v(\tilde{u}, \tilde{v})) \\
&= \big( 
x(u(\tilde{u}, \tilde{v}), v(\tilde{u}, \tilde{v})), 
y(u(\tilde{u}, \tilde{v}), v(\tilde{u}, \tilde{v})),
z(u(\tilde{u}, \tilde{v}), v(\tilde{u}, \tilde{v}))
\big)
\end{aligned}
$$

于是它作为$$\tilde{u}$$、$$\tilde{v}$$的函数仍然是3次以上连续可微的，并且

$$
\begin{aligned}
\boldsymbol{r}_{\tilde{u}} &= \boldsymbol{r}_u \frac{\partial u}{\partial \tilde{u}} + \boldsymbol{r}_v \frac{\partial v}{\partial \tilde{u}} \\
\boldsymbol{r}_{\tilde{v}} &= \boldsymbol{r}_u \frac{\partial u}{\partial \tilde{v}} + \boldsymbol{r}_v \frac{\partial v}{\partial \tilde{v}} \\
\boldsymbol{r}_{\tilde{u}} \times \boldsymbol{r}_{\tilde{v}} &= \frac{\partial (u, v)}{\partial (\tilde{u}, \tilde{v})} \cdot (\boldsymbol{r}_u \times \boldsymbol{r}_v) \neq \mathbf{0}
\end{aligned}
$$

由此可见，在经过如上的变量替换之后，得到的仍然是正则参数曲面。这就是说，正则参数曲面的性质在满足条件(1)、(2)的参数变换下是保持不变的。我们把满足条件(1)、(2)的参数变换称为为容许的参数变换。

### 正则曲面
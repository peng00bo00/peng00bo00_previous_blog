---
layout: article
title: 微分几何笔记03-曲面的第一基本形式
tags: ["CG", "Geometry Processing", "Math"]
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
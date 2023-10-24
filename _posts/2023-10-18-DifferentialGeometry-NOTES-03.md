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
\ \ \ \ , (u, v) \in D
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
\boldsymbol{r}_u (u_0, v_0) = \frac{\partial \boldsymbol{r}}{\partial u} \bigg|_{(u_0, v_0)}, \ \ 
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
\boldsymbol{r}_x \times \boldsymbol{r}_y = \bigg( -\frac{\partial z}{\partial x}, -\frac{\partial z}{\partial y}, 1 \bigg) \neq \mathbf{0}
$$

即Monge形式给出的曲面都是正则的。

### 容许的参数变换

正则参数曲面的参数容许作一定的变换。设

$$
\begin{cases}
u = u(\tilde{u}, \tilde{v}) \\
v = v(\tilde{u}, \tilde{v}) \\
\end{cases}
$$

它们满足如下的条件：

(1) $$u(\tilde{u}, \tilde{v})$$、$$v(\tilde{u}, \tilde{v})$$都是$$\tilde{u}$$、$$\tilde{v}$$的3次以上连续可微函数；

(2) $$\frac{\partial (u, v)}{\partial (\tilde{u}, \tilde{v})} \neq 0$$。

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

我们还规定，向量$$\boldsymbol{r}_u \times \boldsymbol{r}_v$$所指的一侧为曲面的正侧。因此，参数$$u$$，$$v$$的次序决定了正则参数曲面的**定向**。当参数$$u$$，$$v$$的次序颠倒时，向量$$\boldsymbol{r}_u \times \boldsymbol{r}_v$$就改变它的指向，正则参数曲面的定向也随之颠倒。显然，容许的参数变换保持参数曲面的定向不变的充分必要条件是

$$
\frac{\partial (u, v)}{\partial (\tilde{u}, \tilde{v})} \gt 0
$$

### 正则曲面

正则参数曲面的概念在应用中是十分方便、十分广泛的，但是有的曲面却不能够用一张正则参数曲面来表示，而是要把曲面分成若干块，然后每一块用正则参数曲面来表示。因此，正则参数曲面只是表示曲面的一种手段， 正则曲面的概念本身尚需另外定义。

**定义3.1** 设$$S$$是$$\mathbb{E}^3$$的一个子集。如果对于任意一点$$p \in S$$，必存在点$$p$$在$$\mathbb{E}^3$$中的一个邻域$$V \subset \mathbb{E}^3$$，以及$$\mathbb{E}^2$$中的一个区域$$U$$，使得在$$U$$和$$V \cap S$$之间能够建立一一的、双向都是连续的对应，并且该对应$$\boldsymbol{r}: U \rightarrow V \cap S \subset \mathbb{E}^3$$本身是一个正则参数曲面，则称$$S$$是$$\mathbb{E}^3$$中的一张**正则曲面**，简称为**曲面**。
{:.success}

如果曲面$$S$$有两个正则参数表示

$$
\boldsymbol{r}_i: U_i \rightarrow V_i \cap S \subset \mathbb{E}^3, \ \ i = 1,2
$$

使得$$V_1 \cap V_2 \cap S \neq \emptyset$$，那么在任意一点$$p \in V_1 \cap V_2 \cap S$$的附近便有两组曲纹坐标$$(u_1, v_1)$$和$$(u_2, v_2)$$，而且它们之间必定有容许的参数变换。事实上，设

$$
\begin{aligned}
\boldsymbol{r}_1 (u_1, v_1) &= \big( x_1(u_1, v_1), y_1(u_1, v_1), z_1(u_1, v_1) \big), \ \ \forall (u_1, v_1) \in U_1, \\
\boldsymbol{r}_2 (u_2, v_2) &= \big( x_2(u_2, v_2), y_2(u_2, v_2), z_2(u_2, v_2) \big), \ \ \forall (u_2, v_2) \in U_2,
\end{aligned}
$$

那么在点$$p$$的附近有

$$
\begin{aligned}
x &= x_1(u_1, v_1) = x_2(u_2, v_2) \\ 
y &= y_1(u_1, v_1) = y_2(u_2, v_2) \\ 
z &= z_1(u_1, v_1) = z_2(u_2, v_2) \\ 
\end{aligned}
$$

对于函数$$x = x_1(u_1, v_1)$$，$$y = y_1(u_1, v_1)$$，在正则条件

$$
\frac{\partial (x_1, y_1)}{\partial (u_1, v_1)} \neq 0
$$

下，由反函数定理得知，在点$$p$$所对应的参数$$(u_1^0, v_1^0)$$的一个邻域内存在3次以上连续可微的反函数

$$
\begin{cases}
u_1 = f(x, y) \\
v_1 = g(x, y)
\end{cases}
$$

它们满足恒等式

$$
\begin{cases}
f(x_1(u_1, v_1), y_1(u_1, v_1)) \equiv u_1 \\
g(x_1(u_1, v_1), y_1(u_1, v_1)) \equiv v_1
\end{cases}
$$

于是曲纹坐标$$(u_1, v_1)$$和$$(u_2, v_2)$$之间的变换是

$$
\begin{cases}
u_1 = f(x_2(u_2, v_2), y_2(u_2, v_2)) \\
v_1 = g(x_2(u_2, v_2), y_2(u_2, v_2)) \\
\end{cases}
$$

很明显，$$u_1$$、$$v_1$$是$$u_2$$、$$v_2$$的3次以上连续可微函数，并且

$$
\frac{\partial (u_1, v_1)}{\partial (u_2, v_2)} = \frac{\partial (f, g)}{\partial (x, y)} \cdot \frac{\partial (x_2, y_2)}{\partial (u_2, v_2)} = \frac{\partial (x_2, y_2)}{\partial (u_2, v_2)} \bigg( \frac{\partial (x_1, y_1)}{\partial (u_1, v_1)} \bigg)^{-1} \neq 0
$$

因此$$u_1$$、$$v_1$$和$$u_2$$、$$v_2$$之间的参数变换是容许的参数变换。由此可见，在正则曲面上，容许的参数变换是自然而然地出现的，定义在正则曲面上的最应该是与它的正则参数表示无关的量。如果在正则曲面的每一个正则参数表示下都定义了一个量，而它们在容许的参数变换下是保持相等的，则它们便在整个正则曲面上定义了一个完全确定的量。我们要研究的定义在曲面上的量应该具有这种不变性。

如果在正则曲面的每一点的邻域内都能够选定一个正则参数表示，使得在邻域重叠的部分其任意两组参数的变换都保持定向不变，即保持不等式$$\frac{\partial (u_1, v_1)}{\partial (u_2, v_2)} \gt 0$$成立，则称这样的正则曲面是**可定向的**。

在直观上看，每一个正则参数曲面是一个开的曲面片，它与$$\mathbb{E}^2$$中的的一个开区域是同胚的，而正则曲面是把一片片正则参数曲面粘起来的结果。我们研究的重点就是正则参数曲面以及它在容许参数变换下的不变量。

## 切平面和法线

### 切向量

假定正则参数曲面$$S$$的参数方程是$$\boldsymbol{r} = \boldsymbol{r}(u,v)$$。前面介绍过，$$(u, v)$$是曲面$$S$$上的点的曲纹坐标，因此曲面$$S$$上的任意一条连续可微曲线可以用参数方程

$$
\begin{cases}
u = u(t) \\ v = v(t)
\end{cases}
$$

表示，其中$$u(t)$$，$$v(t)$$都是$$t$$的连续可微函数。它作为空间$$\mathbb{E}^3$$中的曲线的参数方程是

$$
\boldsymbol{r} = \boldsymbol{r} (u(t), v(t))
$$

**定义3.2** 曲面$$S$$上经过点$$p$$的任意一条连续可微曲线在该点的切向量称为曲面$$S$$在点$$p$$的**切向量**。
{:.success}

根据定义，曲面$$S$$上经过点$$p$$的$$u$$-曲线和$$v$$-曲线的切向量$$\boldsymbol{r}_u$$和$$\boldsymbol{r}_v$$都是曲面$$S$$在点$$p$$的切向量。假定$$p$$是曲线上对应于$$t = 0$$的点，则曲线在点$$p$$的切向量是

$$
\begin{aligned}
\frac{\mathrm{d} \boldsymbol{r} (u(t), v(t))}{\mathrm{d} t} \bigg|_{t=0} 
&= \bigg( \frac{\partial \boldsymbol{r}}{\partial u} \frac{\mathrm{d} u(t)}{\mathrm{d} t} + \frac{\partial \boldsymbol{r}}{\partial v} \frac{\mathrm{d} v(t)}{\mathrm{d} t} \bigg) \bigg|_{t=0} \\
&= \boldsymbol{r}_u \frac{\mathrm{d} u(t)}{\mathrm{d} t} \bigg|_{t=0} + \boldsymbol{r}_v \frac{\mathrm{d} v(t)}{\mathrm{d} t} \bigg|_{t=0}
\end{aligned}
$$

这意味着曲面$$S$$在点$$p$$的切向量$$\frac{\mathrm{d} \boldsymbol{r} (u(t), v(t))}{\mathrm{d} t} \bigg\vert_{t=0}$$是切向量$$\boldsymbol{r}_u$$和$$\boldsymbol{r}_v$$的线性组合，其组合系数恰好是$$\frac{\mathrm{d} u(t)}{\mathrm{d} t} \bigg\vert_{t=0}$$，$$\frac{\mathrm{d} v(t)}{\mathrm{d} t} \bigg\vert_{t=0}$$。反过来，切向量$$\boldsymbol{r}_u$$和$$\boldsymbol{r}_v$$的任意一个线性组合$$a \boldsymbol{r}_u + b \boldsymbol{r}_v$$，其中$$a$$，$$b$$是任意的实数，必定是曲面$$S$$的一个切向量。事实上，只要考虑曲面$$S$$上的连续可微曲线

$$
\begin{cases}
\begin{aligned}
u(t) &= u_0 + a t \\
v(t) &= v_0 + b t
\end{aligned}
\end{cases}
$$

其中点$$p$$对应的参数是$$(u_0, v_0)$$，则该曲线在点$$p$$的切向量是

$$
\frac{\mathrm{d} \boldsymbol{r} (u(t), v(t))}{\mathrm{d} t} \bigg|_{t=0} = a \boldsymbol{r}_u + b \boldsymbol{r}_v
$$

由此可见，曲面$$S$$在点$$p$$的切向量就是点$$p$$的切向量$$\boldsymbol{r}_u$$和$$\boldsymbol{r}_v$$的任意的线性组合。

### 切平面和法线

对于正则参数曲面，$$\boldsymbol{r}_u \times \boldsymbol{r}_v \neq \mathbf{0}$$，故切向量$$\boldsymbol{r}_u$$和$$\boldsymbol{r}_v$$是线性无关的，因此曲面$$S$$在点$$p$$(设点$$p$$对应的参数是$$(u, v)$$)的全体切向量构成一个二维向量空间，这个向量空间称为曲面$$S$$在点$$p$$的**切空间**，记为$$T_pS$$。$$\{ \boldsymbol{r}_u, \boldsymbol{r}_v \}$$是曲面$$S$$在点$$p$$的切空间$$T_pS$$的基底。在空间$$\mathbf{E}^3$$中经过点$$p$$、有切向量$$\boldsymbol{r}_u$$、$$\boldsymbol{r}_v$$张成的二维平面称为曲面$$S$$在点$$p$$的**切平面**。它的参数方程是

$$
\boldsymbol{X} (\lambda, \mu) = \boldsymbol{r} (u, v) + \lambda \boldsymbol{r}_u (u, v) + \mu \boldsymbol{r}_v (u, v)
$$

其中$$\lambda$$、$$\mu$$是切平面上动点的参数。很明显，该切平面的法向量是

$$
\boldsymbol{n} (u, v) = \frac{\boldsymbol{r}_u (u, v) \times \boldsymbol{r}_v (u, v)}{\vert \boldsymbol{r}_u (u, v) \times \boldsymbol{r}_v (u, v) \vert}
$$

在空间$$\mathbb{E}^3$$中经过点$$p$$、以法向量$$\boldsymbol{n} (u, v)$$为方向向量的直线称为曲面$$S$$在点$$p$$的**法线**，它的参数方程是

$$
\boldsymbol{X} (t) = \boldsymbol{r} (u, v) + t \boldsymbol{n} (u, v)
$$

其中$$t$$是法线上动点的参数。

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/okRmIbT.png" width="80%">
</div>

显然，正则参数曲面$$S$$在点$$p$$的切空间、切平面、法线等概念在曲面的容许参数变换下是不变的，因而与正则曲面的参数表示方式无关。当容许参数变换保持定向时，单位法向量$$\boldsymbol{n} (u,v)$$的指向也是不变的；当容许参数变换翻转定向时，单位法向量$$\boldsymbol{n} (u,v)$$则反转指向。由此可见，在可定向的正则曲面上存在连续可微的单位法向量场，而且只有两个互为反转的单位法向量场。确定取哪一个单位法向量场，就是确定了该曲面的一个定向。

### 自然标架

在正则参数曲面$$S: \boldsymbol{r} = \boldsymbol{r}(u, v)$$上的每一点，借助于它的参数方程定义了一个标架$$\{\boldsymbol{r}(u,v); \boldsymbol{r}_u(u,v), \boldsymbol{r}_v (u, v), \boldsymbol{n}(u, v) \}$$，称为该曲面上的**自然标架**。这样，正则参数曲面$$S: \boldsymbol{r} = \boldsymbol{r}(u, v)$$不仅是依赖参数$$(u, v)$$的点的集合，而且也是在$$\mathbb{E}^3$$中依赖参数$$u$$、$$v$$的这些自然标架的集合，即正则参数曲面不仅是在$$\mathbb{E}^3$$中依赖两个参数的点集，而被进一步看成依赖两个参数的标架族，或者是从区域$$D \subset \mathbb{E}^2$$到$$\mathbb{E}^3$$上的全体标架所构成的12维空间的一个映射。与研究正则参数曲线的情形相仿，对正则参数曲面的研究也可以归结为对自然标架场的研究，我们会在后面进行更深入的介绍。

### 隐式曲面

设$$f(x, y, z)$$是定义在$$\mathbb{E}^3$$上的一个区域$$\tilde{D}$$是的连续可微函数。当

$$
\bigg( \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}, \frac{\partial f}{\partial z} \bigg) \neq \mathbf{0}
$$

时，函数$$f$$的等值面

$$
f(x, y, z) = c
$$

是$$\mathbb{E}^3$$中的一个正则曲面。事实上，若设$$p$$是等值面上的一点，对应的参数是$$(x_0, y_0, z_0)$$，并且假定

$$
\frac{\partial f}{\partial z} \bigg\vert_p \neq 0
$$

则根据隐函数定理，在$$Oxy$$平面上点$$(x_0, y_0)$$的一个邻域$$D$$内存在连续可微函数$$z = g(x, y)$$，使得对应任一点$$(x, y) \in D$$满足

$$
f(x, y, g(x, y)) = c
$$

所以，等值面的参数方程是

$$
\boldsymbol{r} (x, y) = (x, y, g(x, y))
$$

很明显，$$\bigg( \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}, \frac{\partial f}{\partial z} \bigg)$$就是等值面的法向量。实际上，若设$$x = x(t)$$，$$y = y(t)$$，$$z = z(t)$$是等值面上任意一条连续可微曲线$$C$$的参数方程，则对于任意的$$t$$恒等地有

$$
f(x(t), y(t), z(t)) = c
$$

将上式对变量$$t$$求导得到

$$
\frac{\partial f}{\partial x} \frac{\mathrm{d} x(t)}{\mathrm{d} t} + \frac{\partial f}{\partial y} \frac{\mathrm{d} y(t)}{\mathrm{d} t}  + \frac{\partial f}{\partial z} \frac{\mathrm{d} z(t)}{\mathrm{d} t} = 0
$$

这说明向量$$\bigg( \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}, \frac{\partial f}{\partial z} \bigg)$$与曲线$$C$$的切向量$$\bigg( \frac{\mathrm{d} x(t)}{\mathrm{d} t}, \frac{\mathrm{d} y(t)}{\mathrm{d} t}, \frac{\mathrm{d} z(t)}{\mathrm{d} t} \bigg)$$是正交的，因而它与等值面上任意一条连续可微曲线都是垂直的，因此必定是等值面的一个法向量。

### 正则参数曲面的微分

现在有必要对正则参数曲面$$S$$的参数方程$$\boldsymbol{r} = \boldsymbol{r} (u, v)$$的微分$$\mathrm{d} \boldsymbol{r} (u, v)$$作一些说明。首先，$$\boldsymbol{r} = \boldsymbol{r} (u, v)$$的微分$$\mathrm{d} \boldsymbol{r} (u, v)$$是关于参数$$u$$、$$v$$的微分$$\mathrm{d} u$$、$$\mathrm{d} v$$的线性表达式：

$$
\begin{aligned}
\mathrm{d} \boldsymbol{r} (u, v) &= \boldsymbol{r}_u (u, v) \mathrm{d} u + \boldsymbol{r}_v (u, v) \mathrm{d} v \\
&=\boldsymbol{r}_u (u, v) \Delta u + \boldsymbol{r}_v (u, v) \Delta v
\end{aligned}
$$

当$$(\Delta u, \Delta v) \to (0, 0)$$时它是函数$$\boldsymbol{r} (u, v)$$的增量$$\boldsymbol{r} (u + \Delta u, v + \Delta v) - \boldsymbol{r} (u, v)$$作为无穷小量的线性的主要部分，即$$\boldsymbol{r} (u + \Delta u, v + \Delta v) - \boldsymbol{r} (u, v) - \mathrm{d} \boldsymbol{r} (u, v)$$是$$\rho = \sqrt{(\Delta u)^2 + (\Delta v)^2}$$的更高阶的无穷小最，也就是

$$
\lim_{\rho \to 0} \frac{\vert \boldsymbol{r} (u + \Delta u, v + \Delta v) - \boldsymbol{r} (u, v) - \mathrm{d} \boldsymbol{r} (u, v) \vert}{\rho} = 0
$$

另一方面，微分表达式告诉我们$$\mathrm{d} \boldsymbol{r} (u, v)$$是4个自变量$$u$$、$$v$$、$$\mathrm{d} u$$、$$\mathrm{d} v$$的函数，它关于这组新的自变量$$\mathrm{d} u$$、$$\mathrm{d} v$$是线性的。这就是说，$$\mathrm{d} \boldsymbol{r} (u, v)$$是切向量$$\boldsymbol{r}_u (u, v)$$，$$\boldsymbol{r}_v (u, v)$$的线性组合，组合系数是自变量$$\mathrm{d} u$$、$$\mathrm{d} v$$，它们可以取任意的实数值。由此可见，在自变量$$u$$、$$v$$固定的时候，也就是在曲面$$S$$上固定一点的情况下，$$\mathrm{d} \boldsymbol{r}$$代表了曲面$$S$$在点$$\boldsymbol{r}$$处的任意一个切向量，而$$\mathrm{d} u$$、$$\mathrm{d} v$$正是该切向量在自然基底$$\{ \boldsymbol{r}_u (u, v), \boldsymbol{r}_v (u, v) \}$$下的分量，因此它们是切空间$$T_p S$$上的线性函数。为说明这一点，先考察一下一般情形。

我们知道，在一个$$n$$维线性空间$$V$$中取定了一个基底$$\{ \boldsymbol{e}_1, ..., \boldsymbol{e}_n \}$$，则$$V$$中任意一个元素关于该基底的分量是线性空间$$V$$上的线性函数。例如，设

$$
\boldsymbol{w} = w^1 \boldsymbol{e}_1 + ... + w^n \boldsymbol{e}_n
$$

用$$f^i$$表示取向量$$\boldsymbol{w}$$在基底$$\{ \boldsymbol{e}_1, ..., \boldsymbol{e}_n \}$$下第$$i$$个分量的函数，即

$$
f^i (\boldsymbol{w}) = w^i
$$

则$$f^i$$是线性空间$$V$$上的线性函数。实际上，若有另一元素$$\boldsymbol{z} \in V$$，

$$
\boldsymbol{z} = z^1 \boldsymbol{e}_1 + ... + z^n \boldsymbol{e}_n
$$

则

$$
\boldsymbol{w} + \boldsymbol{z} = (w^1 + z^1) \boldsymbol{e}_1 + ... + (w^n + z^n) \boldsymbol{e}_n
$$

因此

$$
f^i (\boldsymbol{w} + \boldsymbol{z}) = w^i + z^i = f^i (\boldsymbol{w}) + f^i (\boldsymbol{z})
$$

对于任意的实数$$\lambda$$有

$$
\lambda \cdot \boldsymbol{w} = (\lambda w^1) \boldsymbol{e}_1 + ... + (\lambda w^n) \boldsymbol{e}_n
$$

因此

$$
f^i (\lambda \cdot \boldsymbol{w}) = \lambda w^i = \lambda \cdot f^i (\boldsymbol{w})
$$

这说明$$f^i$$是线性空间$$V$$上的线性函数。

由此可见，$$\mathrm{d} u$$、$$\mathrm{d} v$$是作为二维线性空间的切空间$$T_p S$$上的线性函数，它们在切向量$$\boldsymbol{X}$$上的值分别是该切向量$$\boldsymbol{X}$$在自然基底$$\{ \boldsymbol{r}_u (u, v), \boldsymbol{r}_v (u, v) \}$$下的分量。这就是说，若设$$\boldsymbol{X} = X^1 \boldsymbol{r}_u + X^2 \boldsymbol{r}_v$$，则

$$
\begin{cases}
\begin{aligned}
\mathrm{d} u (\boldsymbol{X}) &= X^1 \\
\mathrm{d} v (\boldsymbol{X}) &= X^2
\end{aligned}
\end{cases}
$$

在上述意义下，曲面$$S$$在点$$\boldsymbol{r} (u, v)$$处的切平面的方程成为

$$
\boldsymbol{X} = \boldsymbol{r} (u, v) + \boldsymbol{r}_u (u, v) \mathrm{d} u + \boldsymbol{r}_v (u, v) \mathrm{d} v
$$

而$$\mathrm{d} u$$、$$\mathrm{d} v$$成为切平面上动点的参数。因此，在已知正则参数曲面$$S$$的参数方程的前提下，对于固定的$$(u, v)$$来说，$$(\mathrm{d} u, \mathrm{d} v)$$的每一个给定的值对应于由$$\mathrm{d} \boldsymbol{r} = \boldsymbol{r}_u \mathrm{d} u + \boldsymbol{r}_v \mathrm{d} v$$给出的一个确定的切向量，$$(\mathrm{d} u, \mathrm{d} v)$$是该切向量的分量或坐标。此外，我们还经常用比值$$\mathrm{d} u : \mathrm{d} v$$表示曲面$$S$$上的一个切方向。

需要指出的是，一般说来，自然基底$$\{ \boldsymbol{r}_u (u, v), \boldsymbol{r}_v (u, v) \}$$**不是**单位正交的，因而$$(\mathrm{d} u, \mathrm{d} v)$$**不是**切向量在笛卡儿直角坐标系下的分量，两个切向量的内积**不能**写成它们的对应的分量的乘积之和。在下一节，我们将具体地研究切向量的内积的表达式。

## 第一基本形式

根据上一节的讨论我们知道，曲面$$S$$上的任意一点$$p \in S$$处的切空间$$T_p S$$是由切向量$$\boldsymbol{r}_u (u, v)$$，$$\boldsymbol{r}_v (u, v)$$张成的二维向量空间，它是$$\mathbb{R}^3$$的子空间。因此，当曲面$$S$$上的切向量作为$$\mathbb{R}^3$$中的向量时可以求它们的长度和夹角。换言之，曲面$$S$$上任意一点的任意两个切向量的内积就是它们作为$$\mathbb{R}^3$$中的向量的内积。在前面已经说过，曲面$$S$$在任意一点$$\boldsymbol{r} (u, v)$$的任意一个切向量是

$$
\mathrm{d} \boldsymbol{r} (u, v) = \boldsymbol{r}_u (u, v) \mathrm{d} u + \boldsymbol{r}_v (u, v) \mathrm{d} v 
$$

其中$$(\mathrm{d} u, \mathrm{d} v)$$是切向量$$\mathrm{d} \boldsymbol{r} (u, v)$$在自然基底$$\{ \boldsymbol{r}_u (u, v), \boldsymbol{r}_v (u, v) \}$$下的分量。一般说来，$$\{ \boldsymbol{r}_u (u, v), \boldsymbol{r}_v (u, v) \}$$**不是单位正交基底**。但是，如果知道这个基底的度量系数，则切向量$$\mathrm{d} \boldsymbol{r} (u, v)$$与其自身的内积就能够表示成它的分量$$\mathrm{d} u$$、$$\mathrm{d} v$$的二次型。命

$$
\begin{aligned}
E(u, v) &= \boldsymbol{r}_u (u, v) \cdot \boldsymbol{r}_u (u, v) \\
F(u, v) &= \boldsymbol{r}_u (u, v) \cdot \boldsymbol{r}_v (u, v) = \boldsymbol{r}_v (u, v) \cdot \boldsymbol{r}_u (u, v) \\
G(u, v) &= \boldsymbol{r}_v (u, v) \cdot \boldsymbol{r}_v (u, v) \\
\end{aligned}
$$

它们就是基底$$\{ \boldsymbol{r}_u (u, v), \boldsymbol{r}_v (u, v) \}$$的度量系数，称为曲面$$S$$的**第一类基本量**，通常把它们写成一个对称矩阵的形式

$$
\begin{pmatrix}
E & F \\ F & G
\end{pmatrix}
$$

很明显，$$E(u, v) \gt 0$$，$$G(u, v) \gt 0$$，并且

$$
\begin{aligned}
E(u, v) G(u, v) - F^2(u, v) 
&= \vert \boldsymbol{r}_u (u, v) \vert^2 \cdot \vert \boldsymbol{r}_v (u, v) \vert^2 \big( 1 - \cos^2 \angle (\boldsymbol{r}_u (u, v), \boldsymbol{r}_v (u, v) \big) \\
&= \big\vert \boldsymbol{r}_u (u, v) \times \boldsymbol{r}_v (u, v) \big\vert^2 \\
&\gt 0
\end{aligned}
$$

(因为$$\boldsymbol{r}_u (u, v)$$、$$\boldsymbol{r}_v (u, v)$$不共线)，因此对称矩阵$$\begin{pmatrix} E & F \\ F & G \end{pmatrix}$$是一个正定矩阵。命

$$
\begin{aligned}
\mathrm{I} &= \mathrm{d} \boldsymbol{r} (u, v) \cdot \mathrm{d} \boldsymbol{r} (u, v) \\
&= \big( \boldsymbol{r}_u (u, v) \mathrm{d} u + \boldsymbol{r}_v (u, v) \mathrm{d} v  \big) \cdot \big( \boldsymbol{r}_u (u, v) \mathrm{d} u + \boldsymbol{r}_v (u, v) \mathrm{d} v  \big) \\
&= E(u, v) (\mathrm{d} u)^2 + 2F(u, v) \mathrm{d} u \mathrm{d} v + G(u, v) (\mathrm{d} v)^2 \\
&= 
\begin{pmatrix}
\mathrm{d} u, \mathrm{d} v
\end{pmatrix}

\begin{pmatrix}
E & F \\ F & G
\end{pmatrix}

\begin{pmatrix}
\mathrm{d} u \\ \mathrm{d} v
\end{pmatrix}

\end{aligned}
$$

则二次微分式$$\mathrm{I}$$与正则参数曲面$$S$$的参数选取是无关的，称其为曲面$$S$$的**第一基本形式**。

### 第一基本形式的不变性

事实上，根据一次微分的形式不变性，$$\mathrm{d} \boldsymbol{r} (u, v)$$与正则参数曲面$$S$$的参数的选取无关，因此$$\mathrm{I}$$作为$$\mathrm{d} \boldsymbol{r} (u, v)$$与其自身的内积当然也与正则参数曲面$$S$$的参数的选取无关。这个事实也能够从另一个方面进行解释。

假定正则参数曲面$$S: \boldsymbol{r} = \boldsymbol{r} (u, v)$$有一个容许的参数变换

$$
\begin{cases}
u = u(\tilde{u}, \tilde{v}) \\
v = v(\tilde{u}, \tilde{v}) \\
\end{cases}
$$

为方便起见，把曲面$$S$$的新的参数方程仍旧记成

$$
\boldsymbol{r} = \boldsymbol{r} (\tilde{u}, \tilde{v}) = \boldsymbol{r} ( u(\tilde{u}, \tilde{v}), v(\tilde{u}, \tilde{v}))
$$

那么根据求导的链式法则和一次微分的形式不变性，我们有

$$
\begin{aligned}
\mathrm{d} \boldsymbol{r} &= \boldsymbol{r}_u (u, v) \mathrm{d} u + \boldsymbol{r}_v (u, v) \mathrm{d} v  \\
&= \boldsymbol{r}_u (u, v) \bigg( \frac{\partial u}{\partial \tilde{u}} \mathrm{d} \tilde{u} + \frac{\partial u}{\partial \tilde{v}} \mathrm{d} \tilde{v} \bigg) + \boldsymbol{r}_v (u, v) \bigg( \frac{\partial v}{\partial \tilde{u}} \mathrm{d} \tilde{u} + \frac{\partial v}{\partial \tilde{v}} \mathrm{d} \tilde{v} \bigg) \\
&= \boldsymbol{r}_{\tilde{u}} (\tilde{u}, \tilde{v}) \mathrm{d} \tilde{u} + \boldsymbol{r}_{\tilde{v}} (\tilde{u}, \tilde{v}) \mathrm{d} \tilde{v}
\end{aligned}
$$

因此

$$
\begin{aligned}
\boldsymbol{r}_{\tilde{u}} (\tilde{u}, \tilde{v}) &= \boldsymbol{r}_u (u, v) \frac{\partial u}{\partial \tilde{u}} + \boldsymbol{r}_v (u, v) \frac{\partial v}{\partial \tilde{u}} \\
\boldsymbol{r}_{\tilde{v}} (\tilde{u}, \tilde{v}) &= \boldsymbol{r}_u (u, v) \frac{\partial u}{\partial \tilde{v}} + \boldsymbol{r}_v (u, v) \frac{\partial v}{\partial \tilde{v}}
\end{aligned}
$$

并且

$$
\begin{aligned}
\mathrm{d} u &= \frac{\partial u}{\partial \tilde{u}} \mathrm{d} \tilde{u} + \frac{\partial u}{\partial \tilde{v}} \mathrm{d} \tilde{v} \\
\mathrm{d} v &= \frac{\partial v}{\partial \tilde{u}} \mathrm{d} \tilde{u} + \frac{\partial v}{\partial \tilde{v}} \mathrm{d} \tilde{v}
\end{aligned}
$$

将上面两组式子用矩阵来表示，可以得到

$$
\begin{pmatrix}
\boldsymbol{r}_{\tilde{u}} \\ \boldsymbol{r}_{\tilde{v}}
\end{pmatrix}
= J \cdot
\begin{pmatrix}
\boldsymbol{r}_u \\ \boldsymbol{r}_v
\end{pmatrix}
$$

$$
\begin{pmatrix}
\mathrm{d} u & \mathrm{d} v
\end{pmatrix}
=
\begin{pmatrix}
\mathrm{d} \tilde{u} & \mathrm{d} \tilde{v}
\end{pmatrix}
\cdot J
$$

其中

$$
J = 
\begin{pmatrix}
\frac{\partial u}{\partial \tilde{u}} & \frac{\partial v}{\partial \tilde{u}} \\
\frac{\partial u}{\partial \tilde{v}} & \frac{\partial v}{\partial \tilde{v}} \\
\end{pmatrix}
$$

根据曲面$$S$$的第一类基本量的定义

$$
\begin{pmatrix}
E & F \\ F & G
\end{pmatrix}
=
\begin{pmatrix}
\boldsymbol{r}_u \\ \boldsymbol{r}_v
\end{pmatrix}
\cdot
\begin{pmatrix}
\boldsymbol{r}_u & \boldsymbol{r}_v
\end{pmatrix}
$$

因此

$$
\begin{pmatrix}
\tilde{E} & \tilde{F} \\ \tilde{F} & \tilde{G}
\end{pmatrix}
=
\begin{pmatrix}
\boldsymbol{r}_{\tilde{u}} \\ \boldsymbol{r}_{\tilde{v}}
\end{pmatrix}
\cdot
\begin{pmatrix}
\boldsymbol{r}_{\tilde{u}} & \boldsymbol{r}_{\tilde{v}}
\end{pmatrix}
=
J \cdot
\begin{pmatrix}
\tilde{E} & \tilde{F} \\ \tilde{F} & \tilde{G}
\end{pmatrix}
\cdot J^T
$$

所以，曲面$$S$$的第一类基本量的矩阵$$\begin{pmatrix}\tilde{E} & \tilde{F} \\ \tilde{F} & \tilde{G}\end{pmatrix}$$和$$\begin{pmatrix} E & F \\ F & G \end{pmatrix}$$差一个合同变换。

将$$\begin{pmatrix}\tilde{E} & \tilde{F} \\ \tilde{F} & \tilde{G}\end{pmatrix}$$展开则得到

$$
\begin{aligned}
\tilde{E} &= E \bigg( \frac{\partial u}{\partial \tilde{u}} \bigg)^2 + 2F \frac{\partial u}{\partial \tilde{u}} \frac{\partial v}{\partial \tilde{u}} + G \bigg(\frac{\partial v}{\partial \tilde{u}} \bigg)^2 \\
\tilde{F} &= E \frac{\partial u}{\partial \tilde{u}} \frac{\partial u}{\partial \tilde{v}} + F \bigg( \frac{\partial u}{\partial \tilde{u}} \frac{\partial v}{\partial \tilde{v}} + \frac{\partial u}{\partial \tilde{v}} \frac{\partial v}{\partial \tilde{u}} \bigg) + G \frac{\partial v}{\partial \tilde{u}} \frac{\partial v}{\partial \tilde{v}} \\
\tilde{G} &= E \bigg(\frac{\partial u}{\partial \tilde{v}} \bigg)^2 + 2F \frac{\partial u}{\partial \tilde{v}} \frac{\partial v}{\partial \tilde{v}} + G \bigg(\frac{\partial v}{\partial \tilde{v}} \bigg)^2\\
\end{aligned}
$$

类似地

$$
\begin{aligned}
\tilde{E} (\mathrm{d} \tilde{u})^2 + 2 \tilde{F} \mathrm{d} \tilde{u} \mathrm{d} \tilde{v} + \tilde{G} (\mathrm{d} \tilde{v})^2
&=
\begin{pmatrix}
\mathrm{d} \tilde{u} & \mathrm{d} \tilde{v}
\end{pmatrix}
\begin{pmatrix}
\tilde{E} & \tilde{F} \\ \tilde{F} & \tilde{G}
\end{pmatrix}
\begin{pmatrix}
\mathrm{d} \tilde{u} \\ \mathrm{d} \tilde{v}
\end{pmatrix} \\
&=
\begin{pmatrix}
\mathrm{d} \tilde{u} & \mathrm{d} \tilde{v}
\end{pmatrix}
J \cdot
\begin{pmatrix}
E & F \\ F & G
\end{pmatrix}
\cdot J^T
\begin{pmatrix}
\mathrm{d} \tilde{u} \\ \mathrm{d} \tilde{v}
\end{pmatrix} \\
&=
\begin{pmatrix}
\mathrm{d} u & \mathrm{d} v
\end{pmatrix}
\begin{pmatrix}
E & F \\ F & G
\end{pmatrix}
\begin{pmatrix}
\mathrm{d} u \\ \mathrm{d} v
\end{pmatrix} \\
&= 
E (\mathrm{d} u)^2 + 2F \mathrm{d} u \mathrm{d} v + G (\mathrm{d} v)^2 \\
\end{aligned}
$$

即二次微分式$$\mathrm{I}$$与正则参数曲面$$S$$的参数的选取是无关的

### 几何意义

第一基本形式$$\mathrm{I}$$的几何意义是切向量$$\mathrm{d} \boldsymbol{r}$$的长度平方。若在点$$(u, v)$$处有另一个切向量

$$
\delta \boldsymbol{r} (u, v) = \boldsymbol{r}_u (u, v) \delta u + \boldsymbol{r}_v (u, v) \delta v
$$

它的分量是$$\delta u$$、$$\delta v$$，则切向量$$\mathrm{d} \boldsymbol{r}$$和$$\delta \boldsymbol{r}$$的内积是

$$
\begin{aligned}
\mathrm{d} \boldsymbol{r} \cdot \delta \boldsymbol{r} &= \frac{1}{2} \big[ (\mathrm{d} \boldsymbol{r} + \delta \boldsymbol{r} )^2 - (\mathrm{d} \boldsymbol{r})^2 - (\delta \boldsymbol{r})^2 \big] \\
&= E \mathrm{d} u \delta u + F (\mathrm{d} u \delta v + \mathrm{d} v \delta u) + G \mathrm{d} v \delta v
\end{aligned}
$$

为方便起见，有时把上式右端表达式记为$$\mathrm{I} (\mathrm{d} \boldsymbol{r}, \delta \boldsymbol{r})$$。因此

$$
\vert \mathrm{d} \boldsymbol{r} \vert = \sqrt{E (\mathrm{d} u)^2 + 2F \mathrm{d} u \mathrm{d} v + G (\mathrm{d} v)^2} = \sqrt{\mathrm{I} (\mathrm{d} \boldsymbol{r}, \mathrm{d} \boldsymbol{r})}
$$

并且

$$
\begin{aligned}
\cos{\angle (\mathrm{d} \boldsymbol{r}, \delta \boldsymbol{r})} &= \frac{\mathrm{d} \boldsymbol{r} \cdot \delta \boldsymbol{r}}{\vert \mathrm{d} \boldsymbol{r} \vert \vert \delta \boldsymbol{r} \vert} = \frac{\mathrm{I} (\mathrm{d} \boldsymbol{r}, \delta \boldsymbol{r})}{\sqrt{\mathrm{I} (\mathrm{d} \boldsymbol{r}, \mathrm{d} \boldsymbol{r})} \sqrt{\mathrm{I} (\delta \boldsymbol{r}, \delta \boldsymbol{r})}} \\
&= \frac{E \mathrm{d} u \delta u + F (\mathrm{d} u \delta v + \mathrm{d} v \delta u) + G \mathrm{d} v \delta v}{\sqrt{E (\mathrm{d} u)^2 + 2F \mathrm{d} u \mathrm{d} v + G (\mathrm{d} v)^2} \sqrt{E (\delta u)^2 + 2F \delta u \delta v + G (\delta v)^2}}
\end{aligned}
$$

由此可见，切向量$$\mathrm{d} \boldsymbol{r}$$和$$\delta \boldsymbol{r}$$彼此正交的充分必要条件是：

$$
E \mathrm{d} u \delta u + F (\mathrm{d} u \delta v + \mathrm{d} v \delta u) + G \mathrm{d} v \delta v = 0
$$
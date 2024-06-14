---
layout: article
title: 微分几何笔记07-活动标架和外微分法
tags: ["CG", "Geometry Processing", "Math", "Differential Geometry"]
key: DifferentialGeometry-07
aside:
  toc: true
sidebar:
  nav: DifferentialGeometry
---

> 这个系列是北京大学陈维桓教授《微分几何(第二版)》的学习笔记，主要涉及古典微分几何中曲线曲面理论的相关知识。系统学习微分几何对于理解计算机图形学中的各种几何处理算法是十分有益的。本节介绍活动标架和外微分法的相关理论。
<!--more-->

## 外形式

本节要在代数上做一些准备，介绍外形式和外代数的概念。

### 对偶空间

设$$V$$是$$n$$维向量空间，$$\{ \boldsymbol{e}_1, ..., \boldsymbol{e}_n \}$$是它的一个基底，则空间$$V$$中的任意一个元素$$\boldsymbol{x}$$都能够唯一地表示为基底向量$$\boldsymbol{e}_1, ..., \boldsymbol{e}_n$$的线性组合，设为

$$
\boldsymbol{x} = x^1 \boldsymbol{e}_1 + \cdots + x^n \boldsymbol{e}_n \equiv x^i \boldsymbol{e}_i
$$

在最右端我们采用了[Einstein的和式约定](/2023/12/27/DifferentialGeometry-NOTES-05.html#einstein求和约定)。在本节，我们规定所有的指标$$i$$，$$j$$，$$k$$，$$l$$的取值范围是从1到$$n$$的整数。实数$$x^1, ..., x^n$$称为向量$$\boldsymbol{x}$$在基底$$\{ \boldsymbol{e}_1, ..., \boldsymbol{e}_n \}$$下的分量。

设$$f: V \rightarrow \mathbb{R}$$是向量空间$$V$$上的函数。如果对于任意的$$\boldsymbol{x}, \boldsymbol{y} \in V$$及$$\alpha \in \mathbb{R}$$总有

$$
f(\boldsymbol{x} + \boldsymbol{y}) = f(\boldsymbol{x}) + f(\boldsymbol{y}), \ \ \ f(\alpha \cdot \boldsymbol{x}) = \alpha \cdot f(\boldsymbol{x})
$$

则称$$f$$是向量空间$$V$$上的线性函数。在固定的基底$$\{ \boldsymbol{e}_i \}$$下，取向量$$\boldsymbol{x}\in V$$在该基底下的第$$j$$的分量，显然它是在向量空间$$V$$的一个线性函数，记为$$e^j$$，即

$$
e^j (\boldsymbol{x}) = x^j
$$

特别地，函数$$e^j$$在基底向量$$\boldsymbol{e}_i$$上的值是

$$
e^j (\boldsymbol{e}_i) = 
\begin{cases}
1, & i = j \\
0, & i \neq j
\end{cases}
$$

为方便起见，常常把上式右端记为$$\delta_i^j$$，称作Kronecker $$\delta$$记号，即

$$
\delta_i^j = 
\begin{cases}
1, & i = j \\
0, & i \neq j
\end{cases}
$$

这里的$$\delta_i^j$$是专用记号，与基底$$\{ \boldsymbol{e}_i \}$$所用的字母的记号没有关系。

很明显，向量空间$$V$$上的任意两个线性函数的和是$$V$$上的线性函数，$$V$$上的一个线性函数与实数$$\alpha$$的乘积仍然是$$V$$上的线性函数。这就是说，$$V$$上全体线性函数的集合关于加法和数乘法是封闭的。因此该集合是一个新的向量空间，记为$$V^*$$, 称为原向量空间$$V$$的**对偶空间**。容易证明，前面在$$V$$的固定基底$$\{ \boldsymbol{e}_i \}$$下定义的$$n$$个线性函数$$e^1, ..., e^n$$恰好构成空间$$V^*$$的基底，称为与原向量空间$$V$$的基底$$\{ \boldsymbol{e}_1, ..., \boldsymbol{e}_n \}$$对偶的基底。实际上，对于任意的线性函数$$f \in V^*$$和任意的向量$$\boldsymbol{x} = x^i \boldsymbol{e}_i \in V$$，我们有

$$
f(\boldsymbol{x}) = f(x^i \boldsymbol{e}_i) = x^i f(\boldsymbol{e}_i)
$$

命

$$
f_i = f(\boldsymbol{e}_i)
$$

则可以得到

$$
f(\boldsymbol{x}) = f_i x^i = f_i e^i (\boldsymbol{x}) = (f_i e^i) (\boldsymbol{x}), \ \ \ \forall \boldsymbol{x} \in V
$$

因此

$$
f = f_i e^i
$$

这说明向量空间$$V$$上的任意一个线性函数$$f$$能够表示成线性函数$$e^1, ..., e^n$$的线性组合，组合系数$$f_i$$正好是线性函数$$f$$在基底向量$$\boldsymbol{e}_i$$上的值。下面要证明这$$n$$个线性函数$$e^1, ..., e^n$$是线性无关的。假定有$$n$$个实数$$\alpha_1, ..., \alpha_n$$使得线性组合$$\alpha_1 e^1 + \cdots + \alpha_n e^n$$为零，即

$$
\alpha_1 e^1 + \cdots + \alpha_n e^n = 0
$$

将这个零函数在基底$$\boldsymbol{e}_k$$上求值得到

$$
0 = \alpha_i e^i (\boldsymbol{e}_k) = \alpha_i \delta_k^i = \alpha_k, \ \ \ \forall k
$$

这意味着所有的实数$$\alpha_1, ..., \alpha_n$$必须为零，因此线性函数$$e^1, ..., e^n$$是线性无关的，故它们构成对偶向量空间$$V^*$$的基底，特别是$$\dim{V^*} = n$$。$$V$$上的线性函数也称为一次形式，或者1-形式。

### 多重线性函数

类似地，我们可以考虑线性空间$$V$$上的多重线性函数。设

$$
f: \underbrace{V \times \cdots \times V}_{r个} \rightarrow \mathbb{R}
$$

是$$V$$上的$$r$$元函数。如果它对于每一个自变量来说都是线性函数，则称它是$$r$$重线性函数。线性空间$$V$$上全体$$r$$重线性函数的集合关于加法和数乘法自然是封闭的，因此它本身是一个向量空间，记为$$\bigotimes^r V^*$$，或者$$V_r$$。

另外，任意两个多重线性函数能够作张量积，得到一个新的多重线性函数。例如，设$$f$$是一个$$r$$重线性函数，$$g$$是一个$$s$$重线性函数，$$f$$和$$g$$的张量积$$f \otimes g$$定义为

$$
f \otimes g (x_1, ..., x_{r+s}) = f(x_1, ..., x_r) \cdot g(x_{r+1}, ..., x_{r+s})
$$

其中$$x_1, ..., x_{r+s} \in V$$。很明显，$$f \otimes g$$是一个$$r+s$$重线性函数。容易验证，张量积具有分配律和结合律，即

分配率：$$(f+g) \otimes h = f \otimes h + g \otimes h$$，$$h \otimes (f + g) = h \otimes f + h \otimes g$$

结合律：$$(f \otimes g) \otimes h = f \otimes (g \otimes h) = f \otimes g \otimes h$$

因此，$$r$$个线性函数的张量积便成为一个$$r$$重线性函数。特别地，设$$\{ e^1, ..., e^n \}$$是对偶向量空间$$V^*$$的基底，任意固定$$r$$个指标$$i_1, ..., i_r$$，则我们得到一个$$r$$重线性函数$$e^{i_1} \otimes \cdots \otimes e^{i_r}$$，它在向量$$\boldsymbol{x}_1, ..., \boldsymbol{x}_r \in V$$上的值是

$$
e^{i_1} \otimes \cdots \otimes e^{i_r} (\boldsymbol{x}_1, ..., \boldsymbol{x}_r) = e^{i_1} (\boldsymbol{x}_1) \cdots e^{i_r} (\boldsymbol{x}_r) = x_1^{i_1} \cdots x_r^{i_r}
$$

指标$$i_1, ..., i_r$$的选法共有$$n^r$$种，因此我们得到$$n^r$$个$$r$$重线性函数

$$
e^{i_1} \otimes \cdots \otimes e^{i_r}, \ \ \ 1 \leq i_1, ..., i_r \leq n
$$

它们构成向量空间$$\bigotimes^r V^*$$的基底，由此可见$$\dim{\bigotimes^r V^*} = n^r$$。实际上，若设$$f \in \bigotimes^r V^*$$，$$\boldsymbol{x}_1, ..., \boldsymbol{x}_r \in V$$，则

$$
\begin{aligned}
f(\boldsymbol{x}_1, ..., \boldsymbol{x}_r) &= f(x_1^{i_1} \boldsymbol{e}_{i_1}, ..., x_r^{i_r} \boldsymbol{e}_{i_r}) \\
&= x_1^{i_1} \cdots x_r^{i_r} \cdot f(\boldsymbol{e}_{i_1}, ..., \boldsymbol{e}_{i_r}) \\
&= f_{i_1 \cdots i_r} e^{i_1} \otimes \cdots \otimes e^{i_r} (\boldsymbol{x}_1, ..., \boldsymbol{x}_r)
\end{aligned}
$$

其中

$$
f_{i_1 \cdots i_r} = f(\boldsymbol{e}_{i_1}, ..., \boldsymbol{e}_{i_r})
$$

因此

$$
f = f_{i_1 \cdots i_r} e^{i_1} \otimes \cdots \otimes e^{i_r}
$$

类似地，可以证明$$n^r$$个$$r$$重线性函数是线性无关的。

### 外形式

设$$f \in \bigotimes^r V^*$$。如果在函数$$f$$的任意两个自变量交换位置时$$f$$的值只改变它的符号，即对于任意的$$\boldsymbol{x}_1, ..., \boldsymbol{x}_r \in V$$以及任意的$$1 \leq s \lt t \leq r$$总有

$$
\begin{aligned}
f(\boldsymbol{x}_1, ..., \boldsymbol{x}_{s-1}, \boldsymbol{x}_s, \boldsymbol{x}_{s+1}, ..., \boldsymbol{x}_{t-1}, \boldsymbol{x}_t, \boldsymbol{x}_{t+1}, ...) = \\
-f(\boldsymbol{x}_1, ..., \boldsymbol{x}_{s-1}, \boldsymbol{x}_t, \boldsymbol{x}_{s+1}, ..., \boldsymbol{x}_{t-1}, \boldsymbol{x}_s, \boldsymbol{x}_{t+1}, ..)
\end{aligned}
$$

则称$$f$$是一个反对称的$$r$$重线性函数，或称$$f$$是一个$$r$$次**外形式**，简称为$$r$$-形式。此时，如果$$\sigma$$是$$\{ 1, ..., r \}$$的任意一个置换，则有

$$
f(\boldsymbol{x}_{\sigma(1)}, ..., \boldsymbol{x}_{\sigma(r)}) = \text{sign} (\sigma) \cdot f(\boldsymbol{x}_1, ..., \boldsymbol{x}_r)
$$

其中$$\text{sign}(\sigma)$$是置换$$\sigma$$的符号，即

$$
\text{sign} (\sigma) = 
\begin{cases}
1, &\text{若 $\sigma$是偶置换} \\
-1, &\text{若 $\sigma$是奇置换} \\
\end{cases}
$$

实际上，$$r$$次外形式的最简单的例子就是由行列式给出的。

设$$\boldsymbol{x}_1, ..., \boldsymbol{x}_r$$是向量空间$$V$$中的$$r$$个元素，在基底$$\{ \boldsymbol{e}_1, ..., \boldsymbol{e}_n \}$$下它们可以表示为

$$
\boldsymbol{x}_i = x_i^1 \boldsymbol{e}_1 + \cdots + x_i^n \boldsymbol{e}_n
$$

任意取定一组指标$$1 \leq j_1 \lt \cdots \lt j_r \leq n$$，命

$$
D^{j_1 ... j_r} (\boldsymbol{x}_1, ..., \boldsymbol{x}_r) = 
\begin{vmatrix}
x_1^{j_1} & \cdots & x_1^{j_r} \\
\vdots & & \vdots \\
x_r^{j_1} & \cdots & x_r^{j_r} \\
\end{vmatrix}
$$

根据行列式的形式，函数$$D^{j_1 ... j_r} (\boldsymbol{x}_1, ..., \boldsymbol{x}_r)$$是$$\boldsymbol{x}_1, ..., \boldsymbol{x}_r$$的反对称的$$r$$重线性函数，即$$D^{j_1 ... j_r}$$是一个$$r$$次外形式。

### 外积

以后我们要证明任意一个$$r$$次外形式无非是这样的一些行列式的线性组合。为此我们先介绍反对称化运算和外积运算这两个概念。

所谓的反对称化运算是将一个$$r$$重线性函数变成一个$$r$$重反对称线性函数的手段。实际上，$$r$$重线性函数$$f$$的反对称化(记为$$[f]$$)就是将它的自变量做所有的置换，然后取它们的值的交替平均值。例如，设$$f$$是$$V$$上的一个2重线性函数，则

$$
[f] (\boldsymbol{x}, \boldsymbol{y}) = \frac{1}{2} \big( f (\boldsymbol{x}, \boldsymbol{y}) - f (\boldsymbol{y}, \boldsymbol{x}) \big), \ \ \ \forall \boldsymbol{x}, \boldsymbol{y} \in V
$$

如果$$f$$是$$V$$上的一个3重线性函数，则

$$
\begin{aligned}[]
[f] (\boldsymbol{x}, \boldsymbol{y}, \boldsymbol{z}) = \frac{1}{6} \big( &f (\boldsymbol{x}, \boldsymbol{y}, \boldsymbol{z}) - f (\boldsymbol{y}, \boldsymbol{x}, \boldsymbol{z}) + f (\boldsymbol{y}, \boldsymbol{z}, \boldsymbol{x}) \\
- &f (\boldsymbol{z}, \boldsymbol{y}, \boldsymbol{x}) + f (\boldsymbol{z}, \boldsymbol{x}, \boldsymbol{y}) - f (\boldsymbol{x}, \boldsymbol{z}, \boldsymbol{y}) \big)
\end{aligned}
$$

其中$$\forall \boldsymbol{x}, \boldsymbol{y}, \boldsymbol{z} \in V$$。一般地，设$$f$$是$$V$$上的一个$$r$$重线性函数，则

$$
[f] (\boldsymbol{x}_1, ..., \boldsymbol{x}_r) = \frac{1}{r!} \sum_{\sigma \in \mathfrak{G}_r} \text{sign} (\sigma) \cdot f (\boldsymbol{x}_{\sigma(1)}, ..., \boldsymbol{x}_{\sigma(r)})
$$

其中$$\mathfrak{G}_r$$是$$r$$个整数$$\{ 1, ..., r \}$$的置换群。很明显，$$[f]$$是一个$$r$$次外形式。如果$$f$$本身是$$r$$次外形式，则$$[f] = f$$。

向量空间$$V$$上的全体$$r$$次外形式集合记为$$\bigwedge^r V^*$$，因为加法和数乘法在集合$$\bigwedge^r V^*$$中是封闭的，因此它自然是一个向量空间。更要紧的一个事实是在外形式之间还能够定义外积运算， 它在实质上是张量积和反对称化运算的复合。

**定义7.1** 设$$f \in \bigwedge^r V^*$$，$$g \in \bigwedge^s V^*$$，则$$f$$和$$g$$的**外积**$$f \wedge g$$是一个$$(r+s)$$次外形式，定义为$$f \wedge g = \frac{(r+s)!}{r! s!} [f \otimes g]$$。
{:.success}

根据**定义7.1**，设$$f$$、$$g$$是向量空间$$V$$上的两个一次形式，则它们的外积为

$$
\begin{aligned}
f \wedge g (\boldsymbol{x}, \boldsymbol{y}) &= 2 [f \otimes g] (\boldsymbol{x}, \boldsymbol{y}) = f \otimes g (\boldsymbol{x}, \boldsymbol{y}) - f \otimes g (\boldsymbol{y}, \boldsymbol{x}) \\
&= f(\boldsymbol{x}) g(\boldsymbol{y}) - f(\boldsymbol{y}) g(\boldsymbol{x}) \\
&= 
\begin{vmatrix}
f(\boldsymbol{x}) & f(\boldsymbol{y}) \\
g(\boldsymbol{x}) & g(\boldsymbol{y}) \\
\end{vmatrix}
\end{aligned}
$$

其中$$\boldsymbol{x}, \boldsymbol{y} \in V$$。类似地，设$$f$$、$$g$$、$$h$$是向量空间$$V$$上的三个一次形式，它们的外积为

$$
f \wedge (g \wedge h) (\boldsymbol{x}, \boldsymbol{y}, \boldsymbol{z}) = 
\begin{vmatrix}
f(\boldsymbol{x}) & f(\boldsymbol{y}) & f(\boldsymbol{z}) \\
g(\boldsymbol{x}) & g(\boldsymbol{y}) & g(\boldsymbol{z}) \\
h(\boldsymbol{x}) & h(\boldsymbol{y}) & h(\boldsymbol{z}) \\
\end{vmatrix}
$$

**定理7.1** 外积运算遵循下列运算法则：  
(1) 分配率：$$(f_1 + f_2) \wedge g = f_1 \wedge g + f_2 \wedge g$$  
(2) 反交换律：设$$f \in \bigwedge^r V^*$$，$$g \in \bigwedge^s V^*$$，则$$f \wedge g = (-1)^{rs} g \wedge f$$  
(3) 结合律：$$f \wedge (g \wedge h) = (f \wedge g) \wedge h$$  
{:.info}

根据结合律，任意多个外形式的外积是有意义的。例如：3个外形式$$f$$、$$g$$、$$h$$的外积$$f \wedge g \wedge h$$可以写成$$f \wedge (g \wedge h)$$，也可以写成$$(f \wedge g) \wedge h$$。

由反交换律得知，如果$$f$$、$$g$$是$$V$$上的一次形式，则

$$
f \wedge g = - g \wedge f
$$

特别地，

$$
f \wedge f = - f \wedge f = 0
$$

另外，如果在$$f$$、$$g$$中至少有一个是偶次外形式，则下面的交换律成立：

$$
f \wedge g = g \wedge f
$$

现在设$$f^1, ..., f^r$$是$$V$$上的$$r$$个一次形式，则有

$$
f^1 \wedge \cdots \wedge f^r = r! [f^1 \otimes \cdots \otimes f^r]
$$

任意取$$\boldsymbol{x}_1, ..., \boldsymbol{x}_r \in V$$，则

$$
\begin{aligned}
f^1 \wedge \cdots \wedge f^r (\boldsymbol{x}_1, ..., \boldsymbol{x}_r) &= r! [f^1 \otimes \cdots \otimes f^r] (\boldsymbol{x}_1, ..., \boldsymbol{x}_r) \\
&=
\begin{vmatrix}
f^1 (\boldsymbol{x}_1) & \cdots & f^1 (\boldsymbol{x}_r) \\
\vdots & & \vdots \\
f^r (\boldsymbol{x}_1) & \cdots & f^r (\boldsymbol{x}_r) \\
\end{vmatrix}
\end{aligned}
$$

特别地，在$$V^*$$的基底$$\{ e^i \}$$中任意取定$$r$$个成员$$e^{j_1}, ..., e^{j_r}$$，则由上式得到

$$
\begin{aligned}
e^{j_1} \wedge \cdots \wedge e^{j_r} (\boldsymbol{x}_1, ..., \boldsymbol{x}_r) &= 
\begin{vmatrix}
e^{j_1} (\boldsymbol{x}_1) & \cdots & e^{j_1} (\boldsymbol{x}_r) \\
\vdots & & \vdots \\
e^{j_r} (\boldsymbol{x}_1) & \cdots & e^{j_r} (\boldsymbol{x}_r) \\
\end{vmatrix} \\
&=
\begin{vmatrix}
x_1^{j_1} & \cdots & x_r^{j_1} \\
\vdots & & \vdots \\
x_1^{j_r} & \cdots & x_r^{j_r} \\
\end{vmatrix}
\end{aligned}
$$

和前面相对照不难知道

$$
D^{j_1 \cdots j_r} = e^{j_1} \wedge \cdots \wedge e^{j_r}
$$

若在$$V$$的基底$$\{ \boldsymbol{e}_i \}$$中任意取定$$r$$个成员$$e_{i_1}, ..., e_{i_r}$$，则由上面的式子得到

$$
e^{j_1} \wedge \cdots \wedge e^{j_r} (\boldsymbol{e}_{i_1}, ..., \boldsymbol{e}_{i_r}) = 
\begin{vmatrix}
\delta_{i_1}^{j_1} & \cdots & \delta_{i_r}^{j_1} \\
\vdots & & \vdots \\
\delta_{i_1}^{j_r} & \cdots & \delta_{i_r}^{j_r} \\
\end{vmatrix}
\equiv \delta_{i_1 \cdots i_r}^{j_1 \cdots j_r}
$$

我们把$$\delta_{i_1 \cdots i_r}^{j_1 \cdots j_r}$$称为广义的Kronecker $$\delta$$记号。由它的定义式即知

$$
\delta_{i_1 \cdots i_r}^{j_1 \cdots j_r} = 
\begin{cases}
1, &\text{若$i_1, ..., i_r$互不相同，且$j_1, ..., j_r$是$i_1, ..., i_r$的偶排列} \\
-1, &\text{若$i_1, ..., i_r$互不相同，且$j_1, ..., j_r$是$i_1, ..., i_r$的奇排列} \\
0, &\text{其它情形}
\end{cases}
$$

根据反交换律，对于一次形式$$f^1, ..., f^r$$的外积$$f^1 \wedge \cdots \wedge f^r$$，交换其中的任意两个因子，则该外积必反号。所以，对任意的$$\sigma \in \mathfrak{G}_r$$有

$$
\begin{aligned}
f^{\sigma (1)} \wedge \cdots \wedge f^{\sigma (r)} &= \text{sign} (\sigma) \cdot f^1 \wedge \cdots \wedge f^r \\
&= \delta_{1 \cdots r}^{\sigma (1) \cdots \sigma (r)} f^1 \wedge \cdots \wedge f^r
\end{aligned}
$$

### 外代数

**定理7.2** 设$$\{ e^1, ..., e^n \}$$是对偶向量空间$$V^*$$的一个基底，则$$\{ e^{j_1} \wedge \cdots \wedge e^{j_r}, 1\leq j_1 \lt \cdots \lt j_r \leq n \}$$是$$r$$次外形式空间$$\bigwedge^r V^*$$的基底。特别是，空间$$\bigwedge^r V^*$$的维数是$$\dim \bigwedge^r V^* = C_n^r$$。当$$r \gt n$$时，$$\bigwedge^r V^* = \{ 0 \}$$。
{:.info}

**证明** 设$$f \in \bigwedge^r V^*$$，则$$f$$作为[$$r$$重线性函数](/2024/06/08/DifferentialGeometry-NOTES-07.html#多重线性函数)可以表示为
$$
f = f_{j_1 \cdots j_r} e^{j_1} \otimes \cdots \otimes e^{j_r}
$$

其中

$$
f_{j_1 \cdots j_r} = f(\boldsymbol{e}_{j_1}, ..., \boldsymbol{e}_{j_r})
$$

这里$$\{ \boldsymbol{e}_i \}$$是向量空间$$V$$中对偶的基底。因为$$f$$的反对称性，所以系数$$f_{j_1 \cdots j_r}$$关于下指标是反对称的，即

$$
f_{j_{\sigma(1)} \cdots j_{\sigma(r)}} = \text{sign} (\sigma) f_{j_1 \cdots j_r}, \ \ \ \forall \sigma \in \mathfrak{G}_r
$$

因此

$$
\begin{aligned}
f &= [f] = f_{j_1 \cdots j_r} [e^{j_1} \otimes \cdots \otimes e^{j_r}] = \frac{1}{r!} f_{j_1 \cdots j_r} e^{j_1} \wedge \cdots \wedge e^{j_r} \\
&= \sum_{1 \leq j_1 \lt \cdots \lt j_r \leq n} f_{j_1 \cdots j_r} e^{j_1} \wedge \cdots \wedge e^{j_r}
\end{aligned}
$$

这说明任意一个$$r$$次外形式$$f$$都能够表示成$$e^{j_1} \wedge \cdots \wedge e^{j_r}$$，$$1 \leq j_1 \lt \cdots \lt j_r \leq n$$的线性组合。

为了证明这$$C_n^r$$个$$r$$次形式$$e^{j_1} \wedge \cdots \wedge e^{j_r}$$，$$1 \leq j_1 \lt \cdots \lt j_r \leq n$$是线性无关的，假定有一组实数$$_{j_1 \cdots j_r}$$，$$1 \leq j_1 \lt \cdots \lt j_r \leq n$$，使得线性组合

$$
\sum_{1 \leq j_1 \lt \cdots \lt j_r \leq n} f_{j_1 \cdots j_r} e^{j_1} \wedge \cdots \wedge e^{j_r} = 0
$$

将这个零函数在向量$$\boldsymbol{e}_{i_1}, ..., \boldsymbol{e}_{i_r}$$，$$1 \leq i_1 \lt \cdots \lt i_r \leq n$$上求值，得到

$$
\begin{aligned}
0 &= \sum_{1 \leq j_1 \lt \cdots \lt j_r \leq n} f_{j_1 \cdots j_r} e^{j_1} \wedge \cdots \wedge e^{j_r} (\boldsymbol{e}_{i_1}, ..., \boldsymbol{e}_{i_r}) \\
&= \sum_{1 \leq j_1 \lt \cdots \lt j_r \leq n} f_{j_1 \cdots j_r} \delta_{i_1 \cdots i_r}^{j_1 \cdots j_r} = f_{i_1 \cdots i_r}
\end{aligned} 
$$

由此可见，这组实数$$f_{j_1 \cdots j_r}$$，$$1 \leq j_1 \lt \cdots \lt j_r \leq n$$必须全部为零。证毕∎

上面的构造可以从代数上进行抽象。假定$$W$$是任意一个$$n$$维向量空间，它的一个基底是$$\{ \boldsymbol{w}_1, ..., \boldsymbol{w}_n \}$$。把$$\boldsymbol{w}_1, ..., \boldsymbol{w}_n$$看作$$n$$个字母，构造实系数多项式，只是要求字母之间的乘法不是普通的交换乘法，而是反交换乘法。也就是在交换任意两个字母的位置时该乘积变号：

$$
\boldsymbol{w}_i \wedge \boldsymbol{w}_j = - \boldsymbol{w}_j \wedge \boldsymbol{w}_i, \ \ \ \forall 1 \leq i, j \leq n
$$

把这种乘法称为外积，假定多个字母的外积遵循结合律，同时假定分配律也成立。如此得到的多项式称为外多项式。由于

$$
\boldsymbol{w}_i \wedge \boldsymbol{w}_i = - \boldsymbol{w}_i \wedge \boldsymbol{w}_i
$$

故

$$
\boldsymbol{w}_i \wedge \boldsymbol{w}_i = 0, \ \ \ \forall i
$$

因此在外多项式的每一项中同一个字母不能出现两次，于是高于$$n$$次的齐次外多项式必定是零。这样，一次外多项式是字母$$\boldsymbol{w}_1, ..., \boldsymbol{w}_n$$的线性组合，它们构成向量空间$$W$$本身。二次外多项式是$$\boldsymbol{w}_i \wedge \boldsymbol{w}_j$$，$$1 \leq i \lt j \leq n$$的线性组合，它们构成的空间记成$$\bigwedge^2 W$$。一般地，$$k$$次外多项式是

$$
\boldsymbol{w}_{i_1} \wedge \cdots \wedge \boldsymbol{w}_{i_k}, \ \ \ 1 \leq i_i \lt \cdots \lt i_k \leq n
$$

的线性组合，它们构成的空间记成$$\bigwedge^k W$$。零次外多项式定义为实数本身。全体外多项式的集合记为

$$
\bigwedge (W) = \sum_{k=0}^n \bigwedge^k W
$$

其元素是各次外多项式的形式和。在集合$$\bigwedge (W)$$中有加法和外积运算，并且外积运算适合分配律、结合律和反交换律，所以从代数上讲，$$\bigwedge (W)$$是一个结合代数，称为向量空间$$W$$上的**外代数**。

由此可见向量空间$$V$$上的外形式就是其对偶空间$$V^*$$的基底向量$$e^1, ..., e^n$$的外多项式。但是，我们在本节具体地、构造性地定义了外形式的外积，而不只是一种抽象的规定。这就是说，本节叙述的外形式的理论具体地构造出一个外代数。

外多项式的形式化定义的好处在于消除外形式和外积的神秘感。从普通的多项式出发，只要规定字母之间的乘法是反交换的，则所得到的便是外多项式。

具有反交换乘法的代数结构的例子还有：设$$\mathbb{R}^3$$是三维向量空间，"×"是该空间上的向量积(叉积)。容易验证，空间$$\mathbb{R}^3$$关于向量积是一个代数。不过，向量积不具有结合律，而满足所谓的[Jacobi恒等式](https://en.wikipedia.org/wiki/Jacobi_identity)，因此$$\mathbb{R}^3$$关于向量积不是外代数，而是所谓的[李代数](https://en.wikipedia.org/wiki/Lie_algebra)。

最后，我们叙述一个重要的定理，它在微分几何中是十分有用的。

**定理7.3 (Cartan引理)** 设$$\omega^1, ..., \omega^r$$，$$\theta_1, ..., \theta_r$$是$$n$$维向量空间$$V$$的$$2r$$个一次形式，其中$$\omega^1, ..., \omega^r$$是线性无关的。如果恒等式$$\sum_{\alpha = 1}^r \omega^\alpha \wedge \theta_\alpha = 0$$成立，则每一个$$\theta_\alpha$$必定是$$\omega^1, ..., \omega^r$$的线性组合，即$$\theta_\alpha = \sum_{\beta = 1}^r a_{\alpha \beta} \omega^\beta$$，并且组合系数$$a_{\alpha \beta}$$是对称的，即$$a_{\alpha \beta} = a_{\beta \alpha}$$。
{:.info}

**证明** 因为$$\omega^1, ..., \omega^r$$是线性无关的，所以可以把它们扩充成为对偶空间$$V^*$$的一个基底$$\omega^1, ..., \omega^r, \omega^{r+1}, ..., \omega^n$$，因此每一个一次形式$$\theta_\alpha$$可以由该基底表示，命

$$
\theta_\alpha = \sum_{i=1}^n a_{\alpha i} \omega^i
$$

已知空间$$\bigwedge^2 V^*$$的基底是$$\{ \omega^i \wedge \omega^j, 1 \leq i \lt j \leq n \}$$，将上式代入已知条件$$\sum_{\alpha = 1}^r \omega^\alpha \wedge \theta_\alpha = 0$$得到

$$
\begin{aligned}
0 & = \sum_{\alpha = 1}^r \omega^\alpha \wedge \theta_\alpha = \sum_{\alpha = 1}^r \sum_{i = 1}^n a_{\alpha i} \omega^\alpha \wedge \omega^i \\
&= \sum_{\alpha = 1}^r \sum_{\beta = 1}^r a_{\alpha \beta} \omega^\alpha \wedge \omega^\beta + \sum_{\alpha = 1}^r \sum_{\xi = r+1}^n a_{\alpha \xi} \omega^\alpha \wedge \omega^\xi \\
&= \sum_{1 \leq \alpha \lt \beta \leq r} (a_{\alpha \beta} - a_{\beta \alpha}) \omega^\alpha \wedge \omega^\beta + \sum_{\alpha = 1}^r \sum_{\xi = r+1}^n a_{\alpha \xi} \omega^\alpha \wedge \omega^\xi
\end{aligned}
$$

于是所有的组合系数必须为零，即

$$
a_{\alpha \beta} - a_{\beta \alpha} = 0, \ \ \ \forall 1 \leq \alpha \lt \beta \leq r
$$

$$
a _{\alpha \xi} = 0, \ \ \ \forall 1 \leq \alpha \leq r \lt \xi \leq n
$$

这样$$\theta_\alpha$$成为

$$
\theta_\alpha = \sum_{\beta = 1}^r a_{\alpha \beta} \omega^\beta
$$

证毕∎

## 外微分式和外微分

本节的主要内容是介绍外微分式的概念及其外微分运算。为此，我们首先复习曲纹坐标系的概念。

### 曲纹坐标系

设欧式空间$$\mathbb{E}^3$$中的正则曲面$$S$$的参数方程是$$\boldsymbol{r} (u^1, u^2)$$，其中$$(u^1, u^2) \in D \subset \mathbb{E}^2$$，则

$$
\mathrm{d} \boldsymbol{r} = \boldsymbol{r}_\alpha \mathrm{d} u^\alpha
$$

在[前面的章节](/2023/10/18/DifferentialGeometry-NOTES-03.html#正则参数曲面)，我们已经强调$$(u^1, u^2)$$可以作为曲面$$S$$上的点$$p$$的坐标，称为曲面$$S$$上的点$$p$$的曲纹坐标。另外，从上式得知曲面$$S$$在点$$p$$的切空间的基底是$$\{ \boldsymbol{r}_1, \boldsymbol{r}_2 \}$$，而$$(\mathrm{d} u^1, \mathrm{d} u^2)$$是在点$$p$$的任意一个切向量的分量，因此$$\mathrm{d} u^1$$、$$\mathrm{d} u^2$$分别是曲面$$S$$在点$$p$$的切空间$$T_p S$$上的线性函数，它们构成曲面$$S$$在点$$p$$的切空间的对偶空间上与自然基底$$\{ \boldsymbol{r}_1, \boldsymbol{r}_2 \}$$对偶的基底，记为$$\{ \mathrm{d} u^1, \mathrm{d} u^2 \}$$。我们把曲面$$S$$在点$$p$$的切空间$$T_p S$$的对偶空间称为曲面$$S$$在点$$p$$的**余切空间**，记为$$T_p^* S$$。余切空间$$T_p^* S$$中的元素称为曲面$$S$$在点$$p$$的**余切向量**，也就是曲面$$S$$在点$$p$$的切空间上的线性函数。

上面的说法可以搬到欧氏空间$$\mathbb{E}^2$$的一个区域$$D$$上去，得到平面区域$$D$$上的曲纹坐标的概念。设$$(x^1, x^2)$$是平面区域$$D$$上的笛卡尔直角坐标系，$$(u^1, u^2)$$是另一个平面区域$$U$$上的笛卡儿直角坐标系。如果在平面区域$$U$$和$$D$$之间存在一个一一对应，它可以表示为从$$U$$到$$D$$的映射$$f: U \rightarrow D$$, 即

$$
x^1 = f^1 (u^1, u^2), \ \ \ x^2 = f^2 (u^1, u^2)
$$

以及从$$D$$到$$U$$的逆映射$$g: D \rightarrow U$$，即

$$
u^1 = g^1 (x^1, x^2), \ \ \ u^2 = g^2 (x^1, x^2)
$$

并且假定函数$$f^\alpha (u^1, u^2)$$、$$g^\alpha (x^1, x^2)$$都是连续可微的，则称$$(u^1, u^2)$$是平面区域$$D$$上的**曲纹坐标系**。如果让$$u^2$$的值固定，而让$$u^1$$变化，则我们再平面区域$$D$$上得到一条曲线，称为平面区域$$D$$上的一条$$u^1$$-曲线。同理，我们有平面区域$$D$$上的一条$$u^2$$-曲线。由于平面区域$$U$$和$$D$$的点之间是一一对应的，因此经过区域$$D$$上的每一点$$p$$只有一条$$u^1$$-曲线，也只有一条$$u^2$$-曲线。我们把$$u^1$$-曲线的切向量记为$$\frac{\partial}{\partial u^1}$$，把$$u^2$$-曲线的切向量记为$$\frac{\partial}{\partial u^2}$$，于是它们构成区域$$D$$在点$$p$$的切空间的基底，记为$$\{ \frac{\partial}{\partial u^1}, \frac{\partial}{\partial u^2} \}$$，同时区域$$D$$在点$$p$$的余切空间的基底是$$\{ \mathrm{d} u^1, \mathrm{d} u^2 \}$$。在点$$p$$的任意一个余切向量是$$\mathrm{d} u^1$$、$$\mathrm{d} u^2$$的线性组合。

由于映射$$f: U \rightarrow D$$和$$g: D \rightarrow U$$互为逆映射，因此有恒等式

$$
x^\alpha = f^\alpha \big( g^1 (x^1, x^2), g^2 (x^1, x^2) \big), \ \ \ \alpha = 1,2
$$

和恒等式

$$
u^\alpha = g^\alpha \big( f^1 (u^1, u^2), f^2 (u^1, u^2) \big), \ \ \ \alpha = 1,2
$$

因为$$f^\alpha (u^1, u^2)$$，$$g^\alpha (x^1, x^2)$$都是连续可微函数，将$$u^\alpha$$对$$u^\beta$$求导得到

$$
\frac{\partial g^\alpha}{\partial x^\gamma} \frac{\partial f^\gamma}{\partial u^\beta} = \delta_\beta^\alpha
$$

所以Jacobi行列式

$$
\frac{\partial (f^1, f^2)}{\partial (u^1, u^2)} \neq 0
$$

反过来，根据反函数定理，如果有两个连续可微函数

$$
x^1 = f^1 (u^1, u^2), \ \ \ x^2 = f^2 (u^1, u^2)
$$

只要它们的Jacobi行列式$$\frac{\partial (f^1, f^2)}{\partial (u^1, u^2)}$$处处不为零，则在任意一点$$(x_0^1, x_0^2)$$的一个邻域内存在反函数

$$
u^1 = g^1 (x^1, x^2), \ \ \ u^2 = g^2 (x^1, x^2)
$$

使得恒等式成立，因此$$(u^1, u^2)$$可作为区域$$D$$在点$$(x_0^1, x_0^2)$$的邻域内的曲纹坐标。由此可见，平面区域上的曲纹坐标系要比笛卡儿直角坐标系随意得多。克服笛卡儿直角坐标系的局限性是数学发展过程中的重要一步，同时曲纹坐标系的概念又导致微分流形概念的产生。

一般地，设$$(x^1, ..., x^n)$$是$$n$$维欧氏空间$$\mathbb{E}^n$$中的区域$$D$$上的笛卡儿直角坐标系，$$(u^1, ..., u^n)$$是$$n$$维欧氏空间$$\mathbb{E}^n$$中的另一个区域$$U$$上笛卡儿直角坐标系。如果在区域$$U$$和$$D$$之间存在一个一一对应，它可以表示为从$$U$$到$$D$$的映射$$f: U \rightarrow D$$，即

$$
x^1 = f^1 (u^1, ..., u^n), \cdots , x^n = f^n (u^1, ..., u^n)
$$

以及从$$D$$到$$U$$的逆映射$$g: D \rightarrow U$$，即

$$
u^1 = g^1 (x^1, ..., x^n), \cdots , u^n = g^n (x^1, ..., x^n)
$$

并且假定函数$$f^\alpha (u^1, ..., u^n)$$，$$g^\alpha (x^1, ..., x^n)$$都是连续可微的，则称$$(u^1, ..., u^n)$$是区域$$D$$上的曲纹坐标系。区域$$D$$在点$$p$$的切空间的自然基底是$$\{ \frac{\partial}{\partial u^1}, ..., \frac{\partial}{\partial u^n} \}$$，同时区域$$D$$在点$$p$$的余切空间的基底是$$\{ \mathrm{d} u^1, ..., \mathrm{d} u^n \}$$。在点$$p$$的任意一个余切向量是$$\mathrm{d} u^1, ..., \mathrm{d} u^n$$的线性组合。

反过来，根据反函数定理，如果有$$n$$个连续可微函数

$$
x^1 = f^1 (u^1, ..., u^n), \cdots , x^n = f^n (u^1, ..., u^n)
$$

只要它们满足条件

$$
\frac{\partial (f^1, ..., f^n)}{\partial (u^1, ..., u^n)} \neq 0
$$

则在任意一点$$(x_0^1, ..., x_0^n)$$的一个邻域内存在反函数

$$
u^1 = g^1 (x^1, ..., x^n), \cdots , u^n = g^n (x^1, ..., x^n)
$$

使得恒等式

$$
x^\alpha = f^\alpha (g^1 (x^1, ..., x^n), ..., g^n (x^1, ..., x^n)), \ \ \ 1 \leq \alpha \leq n
$$

和恒等式

$$
u^\alpha = g^\alpha (f^1 (u^1, ..., u^n), ..., f^n (u^1, ..., u^n)), \ \ \ 1 \leq \alpha \leq n
$$

成立，因此$$(u^1, ..., u^n)$$可以作为区域$$D$$在点$$(x_0^1, ..., x_0^n)$$的邻域内的曲纹坐标。由此可见，$$\frac{\partial (f^1, ..., f^n)}{\partial (u^1, ..., u^n)} \neq 0$$是函数组$$f^1, ..., f^n$$能够在点$$(x_0^1, ..., x_0^n)$$的邻域内引进曲纹坐标系$$(u^1, ..., u^n)$$的充分必要条件。

在20世纪中叶，所谓的大范围微分几何和大范围分析的课题成为数学研究的热门课题，所考虑的空间不再限于具有笛卡儿直角坐标系的欧氏空间，而只要求这种空间在局部上具有曲纹坐标系，并且容许曲纹坐标系作一定的变换，这种空间就是现在所称的**微分流形**。稍微确切一点说，所谓的$$n$$维微分流形是指由$$n$$维欧氏空间中的一些小块区域一片、一片连续可微地拼接起来得到的空间。这里，"连续可微地拼接起来"的意思是在有些小块区域的某部分可以通过其上面的曲纹坐标的正则的连续可微的函数关系等同起来。当$$n=2$$时，这就是[前面](/2024/04/15/DifferentialGeometry-NOTES-06.html#抽象曲面上的几何学)所叙述的二维光滑流形。以后为方便起见，总是假定连续可微函数指它有连续的任意阶的各种偏导数，有时也称这种函数是光滑函数。在$$n$$维微分流形的每一点有切向量、切空间、余切向量、余切空间的概念，特别地在曲纹坐标系$$(u^1, ..., u^n)$$下$$\{ \mathrm{d} u^1, ..., \mathrm{d} u^n \}$$是$$n$$维微分流形在一点的余切空间的基底。

### 外微分式

现在，我们要给出外微分式的定义。

**定义7.2** 设$$D$$是$$n$$为欧式空间$$\mathbb{E}^n$$中的一个区域，$$(u^1, ..., u^n)$$是区域$$D$$上的曲纹坐标系。如果以连续可微的方式在每一点$$p = (u^1, ..., u^n) \in D$$给定了一个$$r$$次外形式  
$$
\begin{aligned}
\varphi (p) &= \frac{1}{r!} \varphi_{i_1 \cdots i_r} (u^1, ..., u^n) \mathrm{d} u^{i_1} \wedge \cdots \wedge \mathrm{d} u^{i_r} \\
&= \sum_{1 \leq i_1 \lt \cdots \lt i_r \leq n} \varphi_{i_1 \cdots i_r} (u^1, ..., u^n) \mathrm{d} u^{i_1} \wedge \cdots \wedge \mathrm{d} u^{i_r}
\end{aligned}
$$
，  
其中假定系数函数$$\varphi_{i_1 \cdots i_r} (u^1, ..., u^n)$$对于下指标是反对称的，则称$$\varphi$$是定义在$$D$$上的**$$r$$次外微分式**。
{:.success}

在这里，所谓的"以连续可微的方式"是指系数$$\varphi_{i_1 \cdots i_r} (u^1, ..., u^n)$$，$$1 \leq i_1 \lt \cdots \lt i_r \leq n$$是$$u^1, ..., u^n$$的连续可微函数，即$$\varphi_{i_1 \cdots i_r} (u^1, ..., u^n)$$是$$u^1, ..., u^n$$的光滑函数。

设$$f: D \rightarrow \mathbb{R}$$是定义在$$D$$上的连续可微函数，则它的微分

$$
\mathrm{d} f = \frac{\partial f}{\partial u^i} \mathrm{d} u^i
$$

即为区域$$D$$上的1次微分式，因而也是$$D$$上的一个1次外微分式。

设$$S$$是三维欧式空间$$\mathbb{E}^3$$中的一块正则参数曲面，参数方程是

$$
\boldsymbol{r} = \boldsymbol{r} (u^1, u^2)
$$

并且它的第一基本形式是

$$
\mathrm{I} = g_{\alpha \beta} \mathrm{d} u^\alpha \mathrm{d} u^\beta
$$

命

$$
\mathrm{d} \sigma = \sqrt{g_{11} g_{22} - (g_{12})^2} \mathrm{d} u^1 \wedge \mathrm{d} u^2
$$

则$$\mathrm{d} \sigma$$是曲面$$S$$上的一个2次微分式。

容易证明：2次微分式$$\mathrm{d} \sigma$$在曲面$$S$$的保持定向的容许参数变换下是不变的。实际上，如果$$(\tilde{u}^1, \tilde{u}^2)$$是曲面$$S$$的另一个保持定向的参数系，于是$$\tilde{u}^\alpha = \tilde{u}^\alpha (u^1, u^2)$$的至少3次以上连续可微的函数，并且

$$
\frac{\partial (\tilde{u}^1, \tilde{u}^2)}{\partial (u^1, u^2)} \gt 0
$$

假定曲面$$S$$的第一基本形式用新参数$$(\tilde{u}^1, \tilde{u}^2)$$的表达式是

$$
\mathrm{I} = \tilde{g}_{\alpha \beta} \mathrm{d} \tilde{u}^\alpha \mathrm{d} \tilde{u}^\beta
$$

则根据[第一基本形式的不变性](/2023/10/18/DifferentialGeometry-NOTES-03.html#第一基本形式的不变性)，在第一类基本量$$\tilde{g}_{\alpha \beta}$$和$$g_{\alpha \beta}$$之间有关系式

$$
\begin{pmatrix}
g_{11} & g_{12} \\ g_{21} & g_{22}
\end{pmatrix}
=
J \cdot
\begin{pmatrix}
\tilde{g}_{11} & \tilde{g}_{12} \\ \tilde{g}_{21} & \tilde{g}_{22}
\end{pmatrix}
\cdot J^T
$$

其中

$$
J = 
\begin{pmatrix}
\frac{\partial \tilde{u}^1}{\partial u^1} & \frac{\partial \tilde{u}^2}{\partial u^1} \\
\frac{\partial \tilde{u}^1}{\partial u^2} & \frac{\partial \tilde{u}^2}{\partial u^2} \\
\end{pmatrix}
$$

对等式两边取行列式得到

$$
g_{11} g_{22} - (g_{12})^2 = (\det{J})^2 (\tilde{g}_{11} \tilde{g}_{22} - (\tilde{g}_{12})^2)
$$

因此

$$
\sqrt{g_{11} g_{22} - (g_{12})^2} = \vert \det{J} \vert \cdot \sqrt{\tilde{g}_{11} \tilde{g}_{22} - (\tilde{g}_{12})^2}
$$

但是根据已知条件，Jacobi行列式大于0

$$
\det{J} = 
\begin{vmatrix}
\frac{\partial \tilde{u}^1}{\partial u^1} & \frac{\partial \tilde{u}^2}{\partial u^1} \\
\frac{\partial \tilde{u}^1}{\partial u^2} & \frac{\partial \tilde{u}^2}{\partial u^2} \\
\end{vmatrix}
= \frac{\partial (\tilde{u}^1, \tilde{u}^2)}{\partial (u^1, u^2)} \gt 0
$$

所以关于第一基本形式的等式成为

$$
\sqrt{g_{11} g_{22} - (g_{12})^2} = \det{J} \cdot \sqrt{\tilde{g}_{11} \tilde{g}_{22} - (\tilde{g}_{12})^2}
$$

在另一方面，对函数$$\tilde{u}^\alpha (u^1, u^2)$$求微分得到

$$
\mathrm{d} \tilde{u}^\alpha = \frac{\partial \tilde{u}^\alpha}{\partial u^1} \mathrm{d} u^1 + \frac{\partial \tilde{u}^\alpha}{\partial u^2} \mathrm{d} u^2, \ \ \ \alpha = 1, 2
$$

因此

$$
\begin{aligned}
\mathrm{d} \tilde{u}^1 \wedge \mathrm{d} \tilde{u}^2 &= \bigg( \frac{\partial \tilde{u}^1}{\partial u^1} \mathrm{d} u^1 + \frac{\partial \tilde{u}^1}{\partial u^2} \mathrm{d} u^2 \bigg) \wedge \bigg( \frac{\partial \tilde{u}^2}{\partial u^1} \mathrm{d} u^1 + \frac{\partial \tilde{u}^2}{\partial u^2} \mathrm{d} u^2 \bigg) \\
&= \frac{\partial (\tilde{u}^1, \tilde{u}^2)}{\partial (u^1, u^2)} \mathrm{d} u^1 \wedge \mathrm{d} u^2
\end{aligned}
$$

综合前面的推导可以得到

$$
\begin{aligned}
\sqrt{\tilde{g}_{11} \tilde{g}_{22} - (\tilde{g}_{12})^2} \mathrm{d} \tilde{u}^1 \wedge \mathrm{d} \tilde{u}^2 &= \sqrt{\tilde{g}_{11} \tilde{g}_{22} - (\tilde{g}_{12})^2} \frac{\partial (\tilde{u}^1, \tilde{u}^2)}{\partial (u^1, u^2)} \mathrm{d} u^1 \wedge \mathrm{d} u^2 \\
&= \sqrt{g_{11} g_{22} - (g_{12})^2} \mathrm{d} u^1 \wedge \mathrm{d} u^2
\end{aligned}
$$

这就证明了2次微分式$$\mathrm{d} \sigma$$在曲面$$S$$的保持定向的容许参数变换下是不变的。

这个事实蕴涵着一个十分重要的结果。我们在前已经定义过[正则曲面](/2023/10/18/DifferentialGeometry-NOTES-03.html#正则曲面)的概念(**定义3.1**)，它是一片、一片正则参数曲面粘合的结果，在重叠部分会有多个曲纹坐标系，但是在不同的曲纹坐标系之间的变换都是容许的参数变换。上面的断言表明，虽然2次微分式$$\mathrm{d} \sigma$$在曲面$$S$$的每一个参数表示是$$\mathrm{d} \sigma = \sqrt{g_{11} g_{22} - (g_{12})^2} \mathrm{d} u^1 \wedge \mathrm{d} u^2$$，但是它在实际上是定义在整个有向正则曲面$$S$$上的2次外微分式。同样，有向抽象曲面(二维黎曼流形)上也有定义在整个曲面上的2次微分式$$\mathrm{d} \sigma$$。在这里，我们具体地描述了构造定义在整个有向曲面$$S$$上的量的一种方式，即这个量可以用局部坐标来表示、但是与局部坐标系的选择无关。这种方式有普遍意义。

2次外微分式$$\mathrm{d} \sigma$$称为在曲面$$S$$上的**面积元素**，其理由如下：假设在曲纹坐标系$$(u^1, u^2)$$下，在点$$p$$给定两个切向量

$$
\boldsymbol{a} = a^1 \boldsymbol{r}_1 + a^2 \boldsymbol{r}_2, \ \ \
\boldsymbol{b} = b^1 \boldsymbol{r}_1 + b^2 \boldsymbol{r}_2
$$

那么

$$
\begin{aligned}
\mathrm{d} \sigma (\boldsymbol{a}, \boldsymbol{b}) &= \sqrt{g_{11} g_{22} - (g_{12})^2} \mathrm{d} u^1 \wedge \mathrm{d} u^2 (\boldsymbol{a}, \boldsymbol{b}) \\
&= \sqrt{g_{11} g_{22} - (g_{12})^2} \big( \mathrm{d} u^1 (\boldsymbol{a}) \mathrm{d} u^2 (\boldsymbol{b}) - \mathrm{d} u^1 (\boldsymbol{b}) \mathrm{d} u^2 (\boldsymbol{a}) \big) \\
&= \sqrt{g_{11} g_{22} - (g_{12})^2} (a^1 b^2 - b^1 a^2)
\end{aligned}
$$

作切向量$$\boldsymbol{a}$$、$$\boldsymbol{b}$$的向量积得到

$$
\begin{aligned}
\boldsymbol{a} \times \boldsymbol{b} &= (a^1 b^2 - b^1 a^2) \boldsymbol{r}_1 \times \boldsymbol{r}_2 \\
&= (a^1 b^2 - b^1 a^2) \vert \boldsymbol{r}_1 \times \boldsymbol{r}_2 \vert \cdot \boldsymbol{n} \\
&= (a^1 b^2 - b^1 a^2) ( \vert \boldsymbol{r}_1 \vert \cdot \vert \boldsymbol{r}_2 \vert \sin{\angle (\boldsymbol{a} , \boldsymbol{b})} ) \cdot \boldsymbol{n} \\
&= (a^1 b^2 - b^1 a^2) \vert \boldsymbol{r}_1 \vert \cdot \vert \boldsymbol{r}_2 \vert \sqrt{1 - \cos^2{\angle (\boldsymbol{a} , \boldsymbol{b})} } \cdot \boldsymbol{n} \\
&= (a^1 b^2 - b^1 a^2) \sqrt{g_{11} g_{22} - (g_{12})^2} \cdot \boldsymbol{n}
\end{aligned}
$$

因此

$$
\mathrm{d} \sigma (\boldsymbol{a}, \boldsymbol{b}) = \pm \vert \boldsymbol{a} \times \boldsymbol{b} \vert
$$

换言之，$$\mathrm{d} \sigma (\boldsymbol{a}, \boldsymbol{b})$$恰好是切向量$$\boldsymbol{a} \times \boldsymbol{b}$$所张的平行四边形的有向面积。

### 外微分

区域$$D$$上的任意两个同次的外微分式能够以逐点计算的方式作加法和外积运算。对于外微分式来说，更重要的一种运算是外微分，它把$$r$$次外微分式变为一个$$r+1$$次外微分式。

**定义7.3** 设
$$
\varphi = \frac{1}{r!} \varphi_{i_1 \cdots i_r} \mathrm{d} u^{i_1} \wedge \cdots \wedge \mathrm{d} u^{i_r}
$$
是定义在区域$$D$$上的一个$$r$$次外微分式。用如下的方式定义$$r+1$$次外微分式：
$$
\begin{aligned}
\mathrm{d} \varphi &= \frac{1}{r!} \mathrm{d} \varphi_{i_1 \cdots i_r} \mathrm{d} u^{i_1} \wedge \cdots \wedge \mathrm{d} u^{i_r} \\
&= \frac{1}{r!} \frac{\partial \varphi_{i_1 \cdots i_r}}{\partial u^j} \mathrm{d} u^j \wedge \mathrm{d} u^{i_1} \wedge \cdots \wedge \mathrm{d} u^{i_r}
\end{aligned}
$$  
称为$$\varphi$$的**外微分**。如果$$\varphi: D \rightarrow \mathbb{R}$$是定义在$$D$$上的连续可微函数(即零次外微分式)，则它的外微分$$\mathrm{d} \varphi$$就是它的普通微分。
{:.success}

**定理7.4** 外微分运算$$\mathrm{d}$$遵循下面的运算法则：  
(1) $$\mathrm{d}$$是线性算子，即对于任意的外微分式$$\varphi^1$$、$$\varphi^2$$有
$$\mathrm{d} (\varphi^1 + \varphi^2) = \mathrm{d} \varphi^1 + \mathrm{d} \varphi^2$$
，
$$\mathrm{d} (c \cdot \varphi^1) = c \cdot \mathrm{d} \varphi^1, \ \ \ \forall c \in \mathbb{R}
$$  
(2) $$\mathrm{d} \circ \mathrm{d} = 0$$，即对于任意一个外微分式$$\varphi$$，有
$$
\mathrm{d} (\mathrm{d} \varphi) = 0
$$  
(3) 若$$\varphi$$是$$r$$次外微分式，则对于任意一个外微分式$$\psi$$，有
$$
\mathrm{d} (\varphi \wedge \psi) = \mathrm{d} \varphi \wedge \psi + (-1)^r \varphi \wedge \mathrm{d} \psi
$$
{:.info}

关于运算法则(3)有两个特殊情形需要特别强调一些。若$$f$$是定义在区域$$D$$上的零次外微分式，即$$f$$是定义在区域$$D$$上的连续可微函数，则由(3)得到

$$
\mathrm{d} (f \psi) = \mathrm{d} f \wedge \psi + f \mathrm{d} \psi
$$

若$$\varphi$$是定义在区域$$D$$上的一次外微分式，则

$$
\mathrm{d} (\varphi \wedge \psi) = \mathrm{d} \varphi \wedge \psi - \varphi \wedge \mathrm{d} \psi
$$

外微分运算还有一个更重要的性质，也就是外微分$$\mathrm{d}$$与外微分式的参数表示的方式无关，这称为"外微分$$\mathrm{d}$$的形式不变性"，是微积分学中"一次微分的形式不变性"的推广。确切地说我们有下面的定理。

**定理7.5** 设$$\varphi$$是定义在$$n$$维区域$$D$$上的一个$$r$$次外微分式，它在曲纹坐标系$$(u^1, ..., u^n)$$下的表示是  
$$
\varphi = \frac{1}{r!} \varphi_{i_1 \cdots i_r} (u^1, ..., u^n) \mathrm{d} u^{i_1} \wedge \cdots \wedge \mathrm{d} u^{i_r}
$$  
在另一个曲纹坐标系$$(\tilde{u}^1, ..., \tilde{u}^n)$$下的表示是
$$
\varphi = \frac{1}{r!} \tilde{\varphi}_{i_1 \cdots i_r} (\tilde{u}^1, ..., \tilde{u}^n) \mathrm{d} \tilde{u}^{i_1} \wedge \cdots \wedge \mathrm{d} \tilde{u}^{i_r}
$$
，  
其中假定$$\varphi_{i_1 \cdots i_r}$$和$$\tilde{\varphi}_{i_1 \cdots i_r}$$对下指标都是反对称的，则有  
$$
\mathrm{d} \varphi_{i_1 \cdots i_r} \wedge \mathrm{d} u^{i_1} \wedge \cdots \wedge \mathrm{d} u^{i_r} = \mathrm{d} \tilde{\varphi}_{i_1 \cdots i_r} \wedge \mathrm{d} \tilde{u}^{i_1} \wedge \cdots \wedge \mathrm{d} \tilde{u}^{i_r}
$$
{:.info}

**证明** 由于不同的曲纹坐标系之间有容许的坐标变换，设为

$$
\tilde{u}^i = \tilde{u}^i (u^1, ..., u^n), \ \ \ 1 \leq i \leq n
$$

故

$$
\mathrm{d} \tilde{u}^i = \frac{\partial \tilde{u}^i}{\partial u^j} \cdot \mathrm{d} u^j
$$

因此

$$
\begin{aligned}
\varphi_{i_1 \cdots i_r} &(u^1, ..., u^n) \mathrm{d} u^{i_1} \wedge \cdots \wedge \mathrm{d} u^{i_r} \\
&= \tilde{\varphi}_{j_1 \cdots j_r} (\tilde{u}^1, ..., \tilde{u}^n) \mathrm{d} \tilde{u}^{j_1} \wedge \cdots \wedge \mathrm{d} \tilde{u}^{j_r} \\
&= \tilde{\varphi}_{j_1 \cdots j_r} (\tilde{u}^1, ..., \tilde{u}^n) \frac{\partial \tilde{u}^{j_1}}{\partial u^{i_1}} \cdots \frac{\partial \tilde{u}^{j_r}}{\partial u^{i_r}} \mathrm{d} u^{i_1} \wedge \cdots \wedge \mathrm{d} u^{i_r}
\end{aligned}
$$

很明显，$$\tilde{\varphi}_{j_1 \cdots j_r} \frac{\partial \tilde{u}^{j_1}}{\partial \tilde{u}^{i_1}} \cdots \frac{\partial \tilde{u}^{j_r}}{\partial \tilde{u}^{i_r}}$$对于下指标$$i_1, ..., i_r$$仍然是反对称的，因此比较上式的前后两端的系数得到

$$
\varphi_{i_1 \cdots i_r} = \tilde{\varphi}_{j_1 \cdots j_r} \frac{\partial \tilde{u}^{j_1}}{\partial u^{i_1}} \cdots \frac{\partial \tilde{u}^{j_r}}{\partial u^{i_r}}
$$

对上式求微分得到

$$
\begin{aligned}
\mathrm{d} \varphi_{i_1 \cdots i_r} &= \frac{\partial}{\partial u^k} \bigg( \tilde{\varphi}_{j_1 \cdots j_r} \frac{\partial \tilde{u}^{j_1}}{\partial \tilde{u}^{i_1}} \cdots \frac{\partial \tilde{u}^{j_r}}{\partial \tilde{u}^{i_r}} \bigg) \mathrm{d} u^k \\
&= \bigg(
\frac{\partial \tilde{\varphi}_{j_1 \cdots j_r}}{\partial \tilde{u}^l} \frac{\partial \tilde{u}^l}{\partial u^k} \frac{\partial \tilde{u}^{j_1}}{\partial u^{i_1}} \cdots \frac{\partial \tilde{u}^{j_r}}{\partial u^{i_r}} + \tilde{\varphi}_{j_1 \cdots j_r} \frac{\partial^2 \tilde{u}^{j_1}}{\partial u^k \partial u^{i_1}} \cdots \frac{\partial \tilde{u}^{j_r}}{\partial u^{i_r}} \\
&+ \cdots + \tilde{\varphi}_{j_1 \cdots j_r} \frac{\partial \tilde{u}^{j_1}}{\partial u^{i_1}} \cdots \frac{\partial^2 \tilde{u}^{j_r}}{\partial u^k \partial u^{i_r}}
\bigg)
\mathrm{d} u^k
\end{aligned}
$$

所以

$$
\begin{aligned}
\mathrm{d} \varphi_{i_1 \cdots i_r} &\wedge \mathrm{d} u^{i_1} \wedge \cdots \wedge \mathrm{d} u^{i_r} \\
&= \bigg( 
\frac{\partial \tilde{\varphi}_{j_1 \cdots j_r}}{\partial \tilde{u}^l} \frac{\partial \tilde{u}^l}{\partial u^k} \frac{\partial \tilde{u}^{j_1}}{\partial u^{i_1}} \cdots \frac{\partial \tilde{u}^{j_r}}{\partial u^{i_r}} + \tilde{\varphi}_{j_1 \cdots j_r} \frac{\partial^2 \tilde{u}^{j_1}}{\partial u^k \partial u^{i_1}} \cdots \frac{\partial \tilde{u}^{j_r}}{\partial u^{i_r}} \\
&+ \cdots + \tilde{\varphi}_{j_1 \cdots j_r} \frac{\partial \tilde{u}^{j_1}}{\partial u^{i_1}} \cdots \frac{\partial^2 \tilde{u}^{j_r}}{\partial u^k \partial u^{i_r}}
\bigg) \mathrm{d} u^k \wedge \mathrm{d} u^{i_1} \wedge \cdots \wedge \mathrm{d} u^{i_r} \\
&= \frac{\partial \tilde{\varphi}_{j_1 \cdots j_r}}{\partial \tilde{u}^l} \frac{\partial \tilde{u}^l}{\partial u^k} \frac{\partial \tilde{u}^{j_1}}{\partial u^{i_1}} \cdots \frac{\partial \tilde{u}^{j_r}}{\partial u^{i_r}} \mathrm{d} u^k \wedge \mathrm{d} u^{i_1} \wedge \cdots \wedge \mathrm{d} u^{i_r} \\
&= \frac{\partial \tilde{\varphi}_{j_1 \cdots j_r}}{\partial \tilde{u}^l} \mathrm{d} \tilde{u}^l \wedge \mathrm{d} \tilde{u}^{j_1} \wedge \cdots \wedge \mathrm{d} \tilde{u}^{j_r} \\
&= \mathrm{d} \tilde{\varphi}_{j_1 \cdots j_r} \wedge \mathrm{d} \tilde{u}^{j_1} \wedge \cdots \wedge \mathrm{d} \tilde{u}^{j_r}
\end{aligned}
$$

在这里，第二个等号成立的理由是除了第1项以外，其余各项全部为零，例如

$$
\begin{aligned}
\frac{\partial^2 \tilde{u}^{j_1}}{\partial u^k \partial u^{i_1}} &\cdots \frac{\partial \tilde{u}^{j_r}}{\partial u^{i_r}} \mathrm{d} u^k \wedge \mathrm{d} u^{i_1} \wedge \cdots \wedge \mathrm{d} u^{i_r} \\
&= \frac{1}{2} \bigg( \frac{\partial^2 \tilde{u}^{j_1}}{\partial u^k \partial u^{i_1}} - \frac{\partial^2 \tilde{u}^{j_1}}{\partial u^{i_1} \partial u^k} \bigg) \cdots \frac{\partial \tilde{u}^{j_r}}{\partial u^{i_r}} \mathrm{d} u^k \wedge \mathrm{d} u^{i_1} \wedge \cdots \wedge \mathrm{d} u^{i_r} \\
&= 0
\end{aligned}
$$

证毕∎

根据**定理7.5**，外微分实际上是定义在整个正则曲面$$S$$上的算子，或者更一般地，外微分是定义在光滑流形上的算子。因为在这种空间每一点的邻域内有局部坐标系，而在不同的局部坐标系之间有容许的坐标变换，但是外微分算子与局部坐标系的选取无关，所以它是在整个空间上定义好的算子。这就是说，给定一个定义在光滑流形$$M$$上的一个$$r$$次外微分式，尽管在不同的局部坐标系下，外微分式有不同的表达式，但是它们的外微分仍旧是同一个外微分式在相应的局部坐标系下的表达式。因此，外微分运算把定义在整个流形$$M$$上的一个$$r$$次外微分式变成定义在整个流形$$M$$上的一个确定的$$r+l$$次外微分式。

**定理7.5**还可以作一些推广，这在以后十分有用。设有另一个$$m$$维区域$$\tilde{D}$$，曲纹坐标系是$$(\tilde{u}^1, ..., \tilde{u}^m)$$，并且$$\sigma: D \rightarrow \tilde{D}$$是一个连续可微映射，表示为

$$
\tilde{u}^\alpha = \tilde{u}^\alpha (u^1, ..., u^n), \ \ \ \alpha = 1, ..., m
$$

映射$$\sigma$$诱导出一个映射$$\sigma^*$$，它把定义在区域$$\tilde{D}$$上的$$r$$次外微分式变为区域$$D$$上的$$r$$次外微分式。例如，设

$$
\tilde{\varphi} = \frac{1}{r!} \sum_{1 \leq \alpha_1, ..., \alpha_r \leq m} \tilde{\varphi}_{\alpha_1 ... \varphi_r} (\tilde{u}^1, ..., \tilde{u}^m) \mathrm{d} \tilde{u}^{\alpha_1} \wedge \cdots \wedge \mathrm{d} \tilde{u}^{\alpha_r}
$$

则$$\sigma^* \tilde{\varphi}$$是区域$$D$$上的$$r$$次外微分形式，它是把$$\tilde{u}^\alpha$$代入$$\tilde{\varphi}$$式所得到的结果，即

$$
\begin{aligned}
\sigma^* \tilde{\varphi} &= \frac{1}{r!} \tilde{\varphi}_{\alpha_1 ... \varphi_r} (\tilde{u}^1 (u^1, ..., u^n), ..., \tilde{u}^m (u^1, ..., u^n)) \\
&\cdot \frac{\partial \tilde{u}^{\alpha_1}}{\partial u^{i_1}} \cdots \frac{\partial \tilde{u}^{\alpha_r}}{\partial u^{i_r}} \mathrm{d} u^{\alpha_1} \wedge \cdots \wedge \mathrm{d} u^{\alpha_r}
\end{aligned}
$$

其中指标$$\alpha_1, ..., \alpha_r$$的取值范围从1到$$m$$，指标$$i_1, ..., i_r$$的取值范围从1到$$n$$，并且上式使用了Einstein和式约定。通常，我们把$$\sigma^* \tilde{\varphi}$$称为区域$$\tilde{D}$$上的$$r$$次外微分式$$\tilde{\varphi}$$通过映射$$\sigma$$在区域$$D$$上的**拉回**。

**定理7.6** 设$$\sigma: \tilde{D} \rightarrow D$$是连续可微映射，则对区域$$\tilde{D}$$上的任意外微分式$$\tilde{\varphi}$$、$$\tilde{\psi}$$有下面的等式：  
(1) $$\sigma^* (\varphi + \psi) = \sigma^* \varphi + \sigma^* \psi $$  
(2) $$\sigma^* (\varphi \wedge \psi) = \sigma^* \varphi \wedge \sigma^* \psi $$  
(3) $$\sigma^* (\mathrm{d} \varphi) = \mathrm{d} (\sigma^* \varphi)$$
{:.info}

把微积分学中的重积分的被积表达式写成外微分式是更加自然的，因为此时积分的变扯替换公式可以通过直接计算得到。例如，考虑二维区域上的重积分$$\iint_D f(x, y) \ \mathrm{d} x \mathrm{d} y$$，其中的$$\mathrm{d} x \mathrm{d} y$$应该换成$$\mathrm{d} x \wedge \mathrm{d} y$$。如果有变量替换

$$
x = x(u, v), \ \ \ y = y(u, v), \ \ \ (u, v) \in \tilde{D}
$$

则

$$
\mathrm{d} x \wedge \mathrm{d} y = 
\begin{vmatrix}
\frac{\partial x}{\partial u} & \frac{\partial x}{\partial v} \\
\frac{\partial y}{\partial u} & \frac{\partial y}{\partial v} \\
\end{vmatrix}
\mathrm{d} u \wedge \mathrm{d} v = \frac{\partial (x, y)}{\partial (u, v)} \mathrm{d} u \wedge \mathrm{d} v
$$

所以

$$
\iint_D f(x, y) \ \mathrm{d} x \wedge \mathrm{d} y = \iint_{\tilde{D}} f(x(u, v), y(u, v)) \cdot \frac{\partial (x, y)}{\partial (u, v)} \mathrm{d} u \wedge \mathrm{d} v
$$

这正好是二重积分的变量替换么丐飞三重积分的情况是一样的。

### Stokes公式

采用外微分的语言，积分的Green公式、Stokes公式和Gauss 公式可以统一地表述如下：设$$G$$是$$n$$维欧式空间$$\mathbb{E}^n$$中的一个$$r$$维有向曲面上的一个区域，$$\partial G$$是$$G$$的边界，具有从$$G$$诱导的定向，$$\omega$$是定义在$$G$$上的$$r-1$$次外微分式，则有

$$
\int_{\partial G} \omega = \int_G \mathrm{d} \omega
$$

上式统称为**Stokes公式**。

## E³中的标架族

## 曲面上的正交标架场

## 曲面上的曲线
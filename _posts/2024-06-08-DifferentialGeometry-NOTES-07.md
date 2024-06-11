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
f(\boldsymbol{x} + \boldsymbol{y}) = f(\boldsymbol{x}) + f(\boldsymbol{y}), \ \ \ f(\boldsymbol{x}) = \alpha \cdot f(\boldsymbol{x})
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

所谓的反对称化运算是将一个$$r$$重线性函数变成一个$$r$$重反对称线性函数的手段。实际上，$$r$$重线性函数$$f$$的反对称化(记为$$[f_1]$$)就是将它的自变量做所有的置换，然后取它们的值的交替平均值。例如，设$$f$$是$$V$$上的一个2重线性函数，则

$$
[f] (\boldsymbol{x}, \boldsymbol{y}) = \frac{1}{2} \big( f (\boldsymbol{x}, \boldsymbol{y}) - f (\boldsymbol{y}, \boldsymbol{x}) \big), \ \ \ \forall \boldsymbol{x}, \boldsymbol{y} \in V
$$

如果$$f$$是$$V$$上的一个3重线性函数，则

$$
\begin{aligned}
[f] (\boldsymbol{x}, \boldsymbol{y}) = \frac{1}{6} \big( &f (\boldsymbol{x}, \boldsymbol{y}, \boldsymbol{z}) - f (\boldsymbol{y}, \boldsymbol{x}, \boldsymbol{z}) + f (\boldsymbol{y}, \boldsymbol{z}, \boldsymbol{x}) \\
- &f (\boldsymbol{z}, \boldsymbol{y}, \boldsymbol{x}) + f (\boldsymbol{z}, \boldsymbol{x}, \boldsymbol{y}) - f (\boldsymbol{x}, \boldsymbol{z}, \boldsymbol{y}) \big)
\end{aligned}
$$

其中$$\forall \boldsymbol{x}, \boldsymbol{y}, \boldsymbol{z} \in V$$。一般地，设$$f$$是$$V$$上的一个$$r$$重线性函数，则

$$
[f] (\boldsymbol{x}_1, ..., \boldsymbol{x}_r) = \frac{1}{r!} \sum_{\sigma \in \mathfrak{G}_r} \text{sign} (\sigma) \cdot f (\boldsymbol{x}_{\sigma(1)}, ..., \boldsymbol{x}_{\sigma(r)})
$$

其中$$\mathfrak{G}_r$$是$$r$$个整数$$\{ 1, ..., r \}$$的置换群。很明显，$$[f]$$是一个$$r$$次外形式。如果$$f$$本身是$$r$$次外形式，则$$[f] = f$$。

向量空间$$V$$上的全体$$r$$次外形式的几何记为$$\bigwedge^r V^*$$，因为加法和数乘法在集合$$\bigwedge^r V^*$$中是封闭的，因此它自然是一个向量空间。更要紧的一个事实是在外形式之间还能够定义外积运算， 它在实质上是张量积和反对称化运算的复合。

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
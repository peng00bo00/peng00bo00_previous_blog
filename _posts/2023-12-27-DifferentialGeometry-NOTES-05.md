---
layout: article
title: 微分几何笔记05-曲面论基本定理
tags: ["CG", "Geometry Processing", "Math", "Differential Geometry"]
key: DifferentialGeometry-05
aside:
  toc: true
sidebar:
  nav: DifferentialGeometry
---

> 这个系列是北京大学陈维桓教授《微分几何(第二版)》的学习笔记，主要涉及古典微分几何中曲线曲面理论的相关知识。系统学习微分几何对于理解计算机图形学中的各种几何处理算法是十分有益的。本节介绍曲面论基本定理。
<!--more-->

## 自然标架的运动公式

在研究空间曲线时，我们在曲线上曲率不为零的每一个点处附加了一个确定的[Frenet标架](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的曲率和frenet标架)，那么Frenet标架沿曲线运动的状况便反映出曲线本身的弯曲情况。Frenet标架可以通过曲线的参数方程的导数和适当的代数运算显式地表示出来，从而$$\mathbb{E}$$中一条曲线可以转化为$$\mathbb{E}$$上所有的标架构成的空间中的一条曲线。曲线论的基本定理和存在定理都是通过标架空间中的这个单参数标架族进行证明的，因为只有这个单参数标架族在运动时给出的信息才完整地表达曲线的弯曲形状。对于空间中的正则参数曲面$$\boldsymbol{r} = \boldsymbol{r} (u, v)$$，我们也需要以某种确定的方式在每一点附加一个标架，这个标架就是自然标架$$\{ \boldsymbol{r}; \boldsymbol{r}_u, \boldsymbol{r}_v, \boldsymbol{n} \}$$。与曲线的情形不同的是，自然标架和曲面的参数选择是有关系的，而且一般来说自然标架不是正交标架，更不是单位正交标架。当然，我们可以在曲面上取单位正交标架场，如$$\{ \boldsymbol{r}; \boldsymbol{e}_1, \boldsymbol{e}_2, \boldsymbol{n} \}$$，其中$$\boldsymbol{e}_1$$, $$\boldsymbol{e}_1$$是曲面在该点的彼此正交的主方向单位向量。但是，主方向本身并不能够像曲线的Frenet标架那样从曲面的参数方程$$\boldsymbol{r} = \boldsymbol{r}(u, v)$$的偏导数直截了当地显式表示出来。即使我们假定在曲面上取了正交曲率线网作为曲面的参数曲线网，也只能做到$$\boldsymbol{r}_u \parallel \boldsymbol{e}_1$$，$$\boldsymbol{r}_v \parallel \boldsymbol{e}_2$$，而不是$$\boldsymbol{r}_u = \boldsymbol{e}_1$$，$$\boldsymbol{r}_v = \boldsymbol{e}_2$$。由此可见，从自然标架场出发展开我们的理论比较方便。后来Cartan发展了活动标架理论来研究微分几何学，在曲面上可以取任意的标架场，包括单位正交标架场，此时要用"微分"替代"偏导数"，因而相应地要用到外微分方法。我们将在后面介绍Cartan的活动标架和外微分法。

### Einstein求和约定

由于我们要做的是多元函数的偏导数，会出现很多求和式，因此把前面所用的由Gauss引进的记号系统改成所谓的**张量记号系统**是比较方便的。首先，曲面的参数记成带上指标的量，如$$u^1$$，$$u^2$$代替原来的$$u$$，$$v$$。要注意的是，在新的记号系统中，$$\mathrm{d} u^2$$设是参数$$u^2$$的微分，而不是微分$$\mathrm{d} u$$的平方。从上下文来看能够知道我们用的是哪一种记号系统，因此是不会混淆的。这样，曲面$$S$$的参数方程记为

$$
\boldsymbol{r} = \boldsymbol{r} (u^1, u^2)
$$

并且命

$$
\boldsymbol{r}_\alpha = \frac{\partial \boldsymbol{r} (u^1, u^2)}{\partial u^\alpha}, \ \ \ \alpha = 1, 2
$$

(需要指出的是，从现在开始如果没有特别的声明，$$\boldsymbol{r}_1$$和$$\boldsymbol{r}_2$$只表示上式所定义的两个切向量)。于是，曲面$$S$$的单位法向量是

$$
\boldsymbol{n} = \frac{\boldsymbol{r}_1 \times \boldsymbol{r}_2}{\vert \boldsymbol{r}_1 \times \boldsymbol{r}_2 \vert}
$$

这样，参数方程$$\boldsymbol{r} = \boldsymbol{r} (u^1, u^2)$$的微分是

$$
\begin{aligned}
\mathrm{d} \boldsymbol{r} = \mathrm{d} \boldsymbol{r} (u^1, u^2) &= \sum_{\alpha=1}^2 \boldsymbol{r}_\alpha (u^1, u^2) \mathrm{d} u^\alpha \\
&= \boldsymbol{r}_\alpha (u^1, u^2) \mathrm{d} u^\alpha
\end{aligned}
$$

在最后一式中，我们采用了**Einstein求和约定**，即：在一个单项式中，如果同一个指标字母$$\alpha$$出现两次，一次作为上指标，一次作为下指标，则该单项式实际上代表对于$$\alpha=1,2$$的求和式。多对重复的指标字母
表示多重的求和式，例如

$$
S_{\alpha \beta} T^{\alpha \beta \gamma} = \sum_{\alpha = 1}^2 \sum_{\beta = 1}^2 S_{\alpha \beta} T^{\alpha \beta \gamma}
$$

$$
P_\alpha^\alpha = \sum_{\alpha = 1}^2 P_\alpha^\alpha = P_1^1 + P_2^2
$$

在求和式中，求和指标的字母本身并没有实质性意义，它们是所谓的"哑"指标，也可以用别的字母来代替，例如

$$
S_{\alpha \beta} T^{\alpha \beta \gamma} = S_{\xi \eta} T^{\xi \eta \gamma}
$$

但是这里的指标$$\gamma$$**不是**哑指标，不表示求和，左、右两边应该保待一致。另外，在一个求和式中同一个指标字母出现三次以上是没有意义的，例如表达式$$S_\alpha T^{\alpha \alpha}$$的写法是不适当的，如果要表示这样的和式必须写出和号，例如

$$
\sum_{\alpha = 1}^2 S_\alpha T^{\alpha \alpha} = S_1 T^{1 1} + S_2 T^{2 2}
$$

**不能**用Einstein求和约定。在表示多重和式时，Einstein求和约定起到十分重要的简化作用。

### Christoffel记号

## 曲面的唯一性定理

## 曲面论基本方程

## 曲面的存在性定理

## Gauss定理
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

在研究空间曲线时，我们在曲线上曲率不为零的每一个点处附加了一个确定的[Frenet标架](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的曲率和frenet标架)，那么Frenet标架沿曲线运动的状况便反映出曲线本身的弯曲情况。Frenet标架可以通过曲线的参数方程的导数和适当的代数运算显式地表示出来，从而$$\mathbb{E}^3$$中一条曲线可以转化为$$\mathbb{E}^3$$上所有的标架构成的空间中的一条曲线。曲线论的基本定理和存在定理都是通过标架空间中的这个单参数标架族进行证明的，因为只有这个单参数标架族在运动时给出的信息才完整地表达曲线的弯曲形状。对于空间中的正则参数曲面$$\boldsymbol{r} = \boldsymbol{r} (u, v)$$，我们也需要以某种确定的方式在每一点附加一个标架，这个标架就是自然标架$$\{ \boldsymbol{r}; \boldsymbol{r}_u, \boldsymbol{r}_v, \boldsymbol{n} \}$$。与曲线的情形不同的是，自然标架和曲面的参数选择是有关系的，而且一般来说自然标架不是正交标架，更不是单位正交标架。当然，我们可以在曲面上取单位正交标架场，如$$\{ \boldsymbol{r}; \boldsymbol{e}_1, \boldsymbol{e}_2, \boldsymbol{n} \}$$，其中$$\boldsymbol{e}_1$$, $$\boldsymbol{e}_2$$是曲面在该点的彼此正交的主方向单位向量。但是，主方向本身并不能够像曲线的Frenet标架那样从曲面的参数方程$$\boldsymbol{r} = \boldsymbol{r}(u, v)$$的偏导数直截了当地显式表示出来。即使我们假定在曲面上取了正交曲率线网作为曲面的参数曲线网，也只能做到$$\boldsymbol{r}_u \parallel \boldsymbol{e}_1$$，$$\boldsymbol{r}_v \parallel \boldsymbol{e}_2$$，而不是$$\boldsymbol{r}_u = \boldsymbol{e}_1$$，$$\boldsymbol{r}_v = \boldsymbol{e}_2$$。由此可见，从自然标架场出发展开我们的理论比较方便。后来Cartan发展了活动标架理论来研究微分几何学，在曲面上可以取任意的标架场，包括单位正交标架场，此时要用"微分"替代"偏导数"，因而相应地要用到外微分方法。我们将在后面介绍Cartan的活动标架和外微分法。

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

### 张量记号

我们用$$g_{\alpha \beta}$$和$$b_{\alpha \beta}$$分别表示曲面$$S$$的第一类基本量和第二类基本量，即

$$
g_{\alpha \beta} = \boldsymbol{r}_\alpha \cdot \boldsymbol{r}_\beta
$$

$$
b_{\alpha \beta} = \boldsymbol{r}_{\alpha \beta} \cdot \boldsymbol{n} = -\boldsymbol{r}_\alpha \cdot \boldsymbol{n}_\beta = -\boldsymbol{n}_\beta \cdot \boldsymbol{r}_\alpha
$$

其中

$$
\boldsymbol{r}_{\alpha \beta} = \frac{\partial}{\partial u^\beta} \bigg( \frac{\partial \boldsymbol{r} (u^1, u^2)}{\partial u^\alpha} \bigg)
$$

这样，曲面$$S$$的两个基本形式是

$$
\begin{cases}
\begin{aligned}
\mathrm{I} &= g_{\alpha \beta} \ \mathrm{d} u^\alpha \mathrm{d} u^\beta \\
\mathrm{II} &= b_{\alpha \beta} \ \mathrm{d} u^\alpha \mathrm{d} u^\beta \\
\end{aligned}
\end{cases}
$$

另外，记

$$
\begin{cases}
\begin{aligned}
g &= \det (g_{\alpha \beta}) = g_{11} g_{22} - g_{12}^2 \\
b &= \det (b_{\alpha \beta}) = b_{11} b_{22} - b_{12}^2 \\
\end{aligned}
\end{cases}
$$

既然矩阵$$(g_{\alpha \beta})$$是正定的，故它有逆矩阵，记为$$(g^{\alpha \beta})$$，于是

$$
g^{\alpha \beta} g_{\beta \gamma} = \delta_\gamma^\alpha = 
\begin{cases}
\begin{aligned}
1, & &\alpha = \gamma \\
0, & &\alpha \neq \gamma
\end{aligned}
\end{cases}
$$

实际上，根据2×2可逆矩阵的逆矩阵公式，显然有

$$
\begin{pmatrix}
g^{11} & g^{12} \\
g^{21} & g^{22} \\
\end{pmatrix}
=
\frac{1}{g}
\begin{pmatrix}
 g_{22} &-g_{12} \\
-g_{21} & g_{11} \\
\end{pmatrix}
$$

总体来说，Gauss的记号和张量记号对照如下表：

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/dQjRIxf.png" width="80%">
</div>

### Christoffel记号

采用张量记号，正则参数曲面$$S$$上的自然标架成为$$\{ \boldsymbol{r}; \boldsymbol{r}_1, \boldsymbol{r}_2, \boldsymbol{n} \}$$。下面要求自然标架场的运动公式。首先根据定义，标架原点的偏导数是

$$
\frac{\partial \boldsymbol{r}}{\partial u^\alpha} = \boldsymbol{r}_\alpha
$$

另外，既然$$\boldsymbol{r}_1$$，$$\boldsymbol{r}_2$$，$$\boldsymbol{n}$$是线性无关的，而$$\frac{\partial \boldsymbol{r}_\alpha}{\partial u^\beta}$$，$$\frac{\partial \boldsymbol{n}}{\partial u^\beta}$$仍然是空间$$\mathbb{E}^3$$中的向量，因此不妨假定

$$
\begin{cases}
\begin{aligned}
\frac{\partial \boldsymbol{r}_\alpha}{\partial u^\beta} &= \Gamma_{\alpha \beta}^\gamma \boldsymbol{r}_\gamma + C_{\alpha \beta} \boldsymbol{n} \\
\frac{\partial \boldsymbol{n}}{\partial u^\beta} &= D_\beta^\gamma \boldsymbol{r}_\gamma + D_\beta \boldsymbol{n} 
\end{aligned}
\end{cases}
$$

其中$$\Gamma_{\alpha \beta}^\gamma$$，$$C_{\alpha \beta}$$，$$D_\beta^\gamma$$，$$D_\beta$$都是待定的系数函数。

将上面第一式的两边用法向量$$\boldsymbol{n}$$作内积，得到

$$
C_{\alpha \beta} = \frac{\partial \boldsymbol{r}_\alpha}{\partial u^\beta} \cdot \boldsymbol{n} = \boldsymbol{r}_{\alpha \beta} \cdot \boldsymbol{n} = b_{\alpha \beta}
$$

即系数$$C_{\alpha \beta}$$恰好是曲面$$S$$的第二类基本量$$b_{\alpha \beta}$$。将第二式的两边用切向量$$\boldsymbol{r}_\xi$$作内积，得到

$$
\frac{\partial \boldsymbol{n}}{\partial u^\beta} \cdot \boldsymbol{r}_\xi = D_\beta^\gamma \boldsymbol{r}_\gamma \cdot \boldsymbol{r}_\xi = D_\beta^\gamma g_{\gamma \xi}
$$

因此

$$
D_\beta^\gamma g_{\gamma \xi} = -b_{\beta \xi}
$$

$$
D_\beta^\gamma = -b_{\beta \xi} g^{\xi \gamma}
$$

命

$$
b_\beta^\gamma = b_{\beta \xi} g^{\xi \gamma}
$$

把$$b_\beta^\gamma$$看成是将$$b_\beta \gamma$$的指标$$\gamma$$借助于矩阵$$(g^{\alpha \beta})$$上升的结果。这个过程是可逆的，即

$$
b_\beta^\gamma \cdot g_{\gamma \eta} = b_{\beta \xi} g^{\xi \gamma} g_{\gamma \eta} = b_{\beta \xi} \delta_{\eta}^\xi = b_{\beta \eta}
$$

这就是说$$b_{\beta \eta}$$是将$$b_\beta^\eta$$的上指标$$\eta$$借助于矩阵$$(g_{\alpha \beta})$$下降的结果。这样，$$(b_\alpha^\beta)$$这组量和第二类基本量$$(b_{\alpha \beta})$$是彼此决定的，并且系数$$D_\beta^\gamma$$是

$$
D_\beta^\gamma = -b_\beta^\gamma
$$

另外，由于$$\boldsymbol{n}$$是单位向量场，故容易得到$$D_\beta = 0$$。

综上所述，$$\frac{\partial \boldsymbol{r}_\alpha}{\partial u^\beta}$$，$$\frac{\partial \boldsymbol{n}}{\partial u^\beta}$$可以重新表示为

$$
\begin{cases}
\begin{aligned}
\frac{\partial \boldsymbol{r}_\alpha}{\partial u^\beta} &= \Gamma_{\alpha \beta}^\gamma \boldsymbol{r}_\gamma + b_{\alpha \beta} \boldsymbol{n} \\
\frac{\partial \boldsymbol{n}}{\partial u^\beta} &= -b_\beta^\gamma \boldsymbol{r}_\gamma
\end{aligned}
\end{cases}
$$

现在我们来求系数函数$$\Gamma_{\alpha \beta}^\gamma $$。在第一式两边点乘$$\boldsymbol{r}_\xi$$，则得

$$
\boldsymbol{r}_{\alpha \beta} \cdot \boldsymbol{r}_\xi = \Gamma_{\alpha \beta}^\gamma \boldsymbol{r}_\gamma \cdot \boldsymbol{r}_\xi = \Gamma_{\alpha \beta}^\gamma g_{\gamma \xi}
$$

记

$$
\Gamma_{\alpha \beta}^\gamma g_{\gamma \xi} = \Gamma_{\xi \alpha \beta}
$$

则我们有

$$
\Gamma_{\alpha \beta}^\gamma = g^{\gamma \xi} \Gamma_{\xi \alpha \beta}
$$

这就是说，记号$$\Gamma_{\alpha \beta}^\gamma$$的上指标$$\gamma$$可以借助于第一类基本量的矩阵$$(g_{\alpha \beta})$$(以后常常称它为曲面的**度量矩阵**)及其逆矩阵$$(g^{\alpha \beta})$$下降和上升。在这里我们规定，当记号$$\Gamma_{\alpha \beta}^\gamma$$的上指标$$\gamma$$下降时落在下指标的最左边成为$$\Gamma_{\gamma \alpha \beta}$$。这样可以得到

$$
\boldsymbol{r}_{\alpha \beta} \cdot \boldsymbol{r}_\xi = \Gamma_{\xi \alpha \beta}
$$

注意到

$$
\boldsymbol{r}_{\alpha \beta} = \frac{\partial}{\partial u^\beta} \bigg( \frac{\partial \boldsymbol{r}(u^1, u^2)}{\partial u^\alpha} \bigg) = \frac{\partial}{\partial u^\alpha} \bigg( \frac{\partial \boldsymbol{r}(u^1, u^2)}{\partial u^\beta} \bigg) = \boldsymbol{r}_{\beta \alpha}
$$

即函数$$\boldsymbol{r}(u^1, u^2)$$的两次偏导数与求导的次序无关，因此$$\boldsymbol{r}_{\alpha \beta}$$关于下指标$$\alpha$$，$$\beta$$是对称的，于是记号$$\Gamma_{\alpha \beta}^{\gamma}$$和$$\Gamma_{\xi \alpha \beta}$$关于下指标$$\alpha$$，$$\beta$$是对称的，即

$$
\Gamma_{\alpha \beta}^{\gamma} = \Gamma_{\beta \alpha}^{\gamma}
$$

$$
\Gamma_{\xi \alpha \beta} = \Gamma_{\xi \beta \alpha}
$$

对$$g_{\alpha \beta} = \boldsymbol{r}_\alpha \cdot \boldsymbol{r}_\beta$$求偏导数得到

$$
\frac{\partial g_{\alpha \beta}}{\partial u^\gamma} = \boldsymbol{r}_{\alpha \gamma} \cdot \boldsymbol{r}_\beta + \boldsymbol{r}_\alpha \cdot \boldsymbol{r}_{\beta \gamma}
$$

带入$$\Gamma_{\gamma \alpha \beta}$$的定义式$$\boldsymbol{r}_{\alpha \beta} \cdot \boldsymbol{r}_\gamma = \Gamma_{\gamma \alpha \beta}$$得到

$$
\frac{\partial g_{\alpha \beta}}{\partial u^\gamma} = \Gamma_{\beta \alpha \gamma} + \Gamma_{\alpha \beta \gamma}
$$

将下指标进行调换得到

$$
\begin{cases}
\begin{aligned}
\frac{\partial g_{\alpha \gamma}}{\partial u^\beta} &= \Gamma_{\gamma \alpha \beta} + \Gamma_{\alpha \gamma \beta} \\
\frac{\partial g_{\gamma \beta}}{\partial u^\alpha} &= \Gamma_{\beta \gamma \alpha} + \Gamma_{\gamma \beta \alpha} \\
\end{aligned}
\end{cases}
$$

将两式相加再减去$$\frac{\partial g_{\alpha \beta}}{\partial u^\gamma}$$，并且利用$$\Gamma_{\gamma \alpha \beta}$$关于后两个下指标的对称性，则得

$$
2 \Gamma_{\gamma \alpha \beta} = \frac{\partial g_{\alpha \gamma}}{\partial u^\beta} + \frac{\partial g_{\gamma \beta}}{\partial u^\alpha} - \frac{\partial g_{\alpha \beta}}{\partial u^\gamma}
$$

或者

$$
\Gamma_{\gamma \alpha \beta} = \frac{1}{2} \bigg( \frac{\partial g_{\alpha \gamma}}{\partial u^\beta} + \frac{\partial g_{\gamma \beta}}{\partial u^\alpha} - \frac{\partial g_{\alpha \beta}}{\partial u^\gamma} \bigg)
$$

因此

$$
\Gamma_{\alpha \beta}^\gamma = \frac{1}{2} g^{\gamma \xi} \bigg( \frac{\partial g_{\alpha \xi}}{\partial u^\beta} + \frac{\partial g_{\xi \beta}}{\partial u^\alpha} - \frac{\partial g_{\alpha \beta}}{\partial u^\xi} \bigg)
$$

由此可见，系数函数$$\Gamma_{\alpha \beta}^\gamma$$是由曲面$$S$$的第一类基本量及其一阶偏导数决定的。通常把上式所定义的$$\Gamma_{\alpha \beta}^\gamma$$称为由曲面$$S$$的度量矩阵$$(g_{\alpha \beta})$$决定的**Christoffel记号**。

### 自然标架场的运动公式

我们将

$$
\begin{cases}
\begin{aligned}
\frac{\partial \boldsymbol{r}}{\partial u^\alpha} &= \boldsymbol{r}_\alpha \\
\frac{\partial \boldsymbol{r}_\alpha}{\partial u^\beta} &= \Gamma_{\alpha \beta}^\gamma \boldsymbol{r}_\gamma + b_{\alpha \beta} \boldsymbol{n} \\
\frac{\partial \boldsymbol{n}}{\partial u^\beta} &= -b_\beta^\gamma \boldsymbol{r}_\gamma
\end{aligned}
\end{cases}
$$

称为曲面$$S$$上自然标架场$$\{ \boldsymbol{r}; \boldsymbol{r}_1, \boldsymbol{r}_2, \boldsymbol{n} \}$$的**运动公式**。通常把第二式$$\frac{\partial \boldsymbol{r}_\alpha}{\partial u^\beta} = \Gamma_{\alpha \beta}^\gamma \boldsymbol{r}_\gamma + b_{\alpha \beta} \boldsymbol{n}$$称为曲面的**Gauss公式**，把第三式$$\frac{\partial \boldsymbol{n}}{\partial u^\beta} = -b_\beta^\gamma \boldsymbol{r}_\gamma$$称为曲面的**Weingarten公式**。容易知道，Weingarten公式正是[Weingarten映射$$W$$的表达式](/2023/11/10/DifferentialGeometry-NOTES-04.html#gauss曲率的几何意义)：

$$
\begin{pmatrix}
\boldsymbol{n}_u \\ \boldsymbol{n}_v
\end{pmatrix}
= -
\begin{pmatrix}
W_{11} & W_{12} \\
W_{21} & W_{22} \\
\end{pmatrix}
\begin{pmatrix}
\boldsymbol{r}_u \\ \boldsymbol{r}_v
\end{pmatrix}
$$

$$
W = 
\begin{pmatrix}
L & M \\
M & N \\
\end{pmatrix}
\begin{pmatrix}
E & F \\
F & G \\
\end{pmatrix}^{-1}
$$

这就是说，$$(b_j^i)$$是Weingarten映射$$W$$在自然基底$$\{ \boldsymbol{r}_1, \boldsymbol{r}_2 \}$$下的矩阵：

$$
b_j^i = W_{i j} = b_{j k} g^{k i}
$$

从上面的公式可以看出，曲面$$S$$上的自然标架场$$\{ \boldsymbol{r}; \boldsymbol{r}_1, \boldsymbol{r}_2, \boldsymbol{n} \}$$沿参数曲线的运动公式是由曲面$$S$$的第一类基本量和第二类基本量完全确定的。要记住，$$\Gamma_{\alpha \beta}^\gamma$$的几何意义是向量$$\boldsymbol{r}_{\alpha \beta}$$用自然标架分解时在切向量$$\boldsymbol{r}_\gamma$$上的分量，而$$\Gamma_{\gamma \alpha \beta}$$的几何意义是向量$$\boldsymbol{r}_{\alpha \beta}$$在切向量$$\boldsymbol{r}_\gamma$$上的正交投影。因此，在求$$\Gamma_{\gamma \alpha \beta}$$时，我们既可以以根据曲面的度量矩阵按照定义式

$$
\Gamma_{\gamma \alpha \beta} = \frac{1}{2} \bigg( \frac{\partial g_{\alpha \gamma}}{\partial u^\beta} + \frac{\partial g_{\gamma \beta}}{\partial u^\alpha} - \frac{\partial g_{\alpha \beta}}{\partial u^\gamma} \bigg)
$$

进行计算，也可以根据曲面的参数方程依据它的几何意义进行计算。

恢复用Gauss曲面论的记法，则Christoffel记号是

$$
\begin{aligned}
\Gamma_{111} &= \frac{1}{2} \frac{\partial E}{\partial u} &\Gamma_{112} &= \Gamma_{121} = \frac{1}{2} \frac{\partial E}{\partial v} \\
\Gamma_{122} &= \frac{\partial F}{\partial u} - \frac{1}{2} \frac{\partial G}{\partial u} &\Gamma_{211} &= \frac{\partial F}{\partial u} - \frac{1}{2} \frac{\partial E}{\partial v} \\
\Gamma_{212} &= \Gamma_{221} =  \frac{1}{2} \frac{\partial G}{\partial u} &\Gamma_{222} &= \frac{1}{2} \frac{\partial G}{\partial v}
\end{aligned}
$$

以及

$$
\begin{aligned}
\Gamma_{11}^1 &= \frac{1}{EG - F^2} \bigg( \frac{G}{2} \frac{\partial E}{\partial u} + \frac{F}{2} \frac{\partial E}{\partial v} - F \frac{\partial F}{\partial u} \bigg) \\
\Gamma_{12}^1 &= \Gamma_{21}^1 = \frac{1}{EG - F^2} \bigg( \frac{G}{2} \frac{\partial E}{\partial v} - \frac{F}{2} \frac{\partial G}{\partial u} \bigg) \\
\Gamma_{22}^1 &= \frac{1}{EG - F^2} \bigg( G \frac{\partial F}{\partial u} - \frac{G}{2} \frac{\partial G}{\partial u} - \frac{F}{2} \frac{\partial G}{\partial v} \bigg) \\
\Gamma_{11}^2 &= \frac{1}{EG - F^2} \bigg( -\frac{F}{2} \frac{\partial E}{\partial u} - \frac{E}{2} \frac{\partial E}{\partial v} + E \frac{\partial F}{\partial u} \bigg) \\
\Gamma_{12}^2 &= \Gamma_{21}^2 = \frac{1}{EG - F^2} \bigg( -\frac{F}{2} \frac{\partial E}{\partial v} + \frac{E}{2} \frac{\partial G}{\partial u} \bigg) \\
\Gamma_{22}^2 &= \frac{1}{EG - F^2} \bigg( -F \frac{\partial F}{\partial v} + \frac{F}{2} \frac{\partial G}{\partial u} + \frac{E}{2} \frac{\partial G}{\partial v} \bigg) \\
\end{aligned}
$$

如果在曲面上取正交参数曲线网，则$$F \equiv 0$$，上面的公式便简化成为

$$
\begin{aligned}
\Gamma_{11}^1 &= \frac{1}{2} \frac{\partial \log E}{\partial u} &\Gamma_{12}^1 &= \Gamma_{21}^1 = \frac{1}{2} \frac{\partial \log E}{\partial v} \\
\Gamma_{22}^1 &= -\frac{1}{2E} \frac{\partial G}{\partial u} &\Gamma_{11}^2 &= -\frac{1}{2G} \frac{\partial E}{\partial v} \\
\Gamma_{12}^2 &= \Gamma_{21}^2 = \frac{1}{2} \frac{\partial \log G}{\partial u} &\Gamma_{22}^2 &= \frac{1}{2} \frac{\partial \log G}{\partial v}
\end{aligned}
$$

通常，求曲面的Christoffel记号是用曲面的第一类基本量，套用上面的公式进行计算。但是如果知道曲面的参数方程则也可以借助于Christoffel记号的几何意义直接来求。

## 曲面的唯一性定理

利用上一节所介绍的曲面上的自然标架场的运动公式，可以直接地证明，曲面在不计空间位置的情况下是由它的第一基本形式和第二基本形式唯一地确定的。

**定理5.1** 设$$S_1$$、$$S_2$$是定义在同一个参数区域$$D \subset \mathbb{E}^2$$上的两个正则参数曲面。若在每一点$$(u^1, u^2) \in D$$，曲面$$S_1$$、$$S_2$$都有相同的第一基本形式和第二基本形式，则曲面$$S_1$$、$$S_2$$在空间$$\mathbb{E}^3$$的一个刚体运动下是彼此重合的。
{:.info}

**证明** 因为$$S_1$$、$$S_2$$上采用了同一组参数，因此在每一点$$u = (u^1, u^2) \in D$$处曲面$$S_1$$和$$S_2$$都有相同的第一基本形式和第二基本形式的意思是，它们在每一点都有相同的第一类基本量和第二类基本量。

假定曲面$$S_i$$的自然标架场是$$\{ \boldsymbol{r}^{(i)}; \boldsymbol{r}_1^{(i)}, \boldsymbol{r}_2^{(i)}, \boldsymbol{n}^{(i)} \}$$，$$i=1,2$$，任意地取定一点$$u_0 = (u_0^1, u_0^2) \in D$$，则由假定得知

$$
\begin{aligned}
\boldsymbol{r}_{\alpha}^{(1)} (u_0) \cdot \boldsymbol{r}_{\beta}^{(1)} (u_0) &= \boldsymbol{r}_{\alpha}^{(2)} (u_0) \cdot \boldsymbol{r}_{\beta}^{(2)} (u_0) = g_{\alpha \beta} (u_0) \\
\boldsymbol{r}_{\alpha}^{(1)} (u_0) \cdot \boldsymbol{n}^{(1)} (u_0) &= \boldsymbol{r}_{\alpha}^{(2)} (u_0) \cdot \boldsymbol{n}^{(2)} (u_0) = 0 \\
\boldsymbol{n}^{(1)} (u_0) \cdot \boldsymbol{n}^{(1)} (u_0) &= \boldsymbol{n}^{(2)} (u_0) \cdot \boldsymbol{n}^{(2)} (u_0) = 1 \\
\end{aligned}
$$

并且$$\{ \boldsymbol{r}^{(i)} (u_0); \boldsymbol{r}_1^{(i)} (u_0), \boldsymbol{r}_2^{(i)} (u_0), \boldsymbol{n}^{(i)} (u_0) \}$$，$$i=1,2$$，都是右手系。这就是说，这两个标架具有相同的度最系数和定向，因而在空间$$\mathrm{E}^3$$中存在一个刚体运动$$\sigma$$，把标架$$\{ \boldsymbol{r}^{(2)} (u_0); \boldsymbol{r}_1^{(2)} (u_0), \boldsymbol{r}_2^{(2)} (u_0), \boldsymbol{n}^{(2)} (u_0) \}$$变长标架$$\{ \boldsymbol{r}^{(1)} (u_0); \boldsymbol{r}_1^{(1)} (u_0), \boldsymbol{r}_2^{(1)} (u_0), \boldsymbol{n}^{(1)} (u_0) \}$$ (参见[定理1.1](/2023/07/30/DifferentialGeometry-NOTES-01.html#正交标架))。

证毕∎

上面的定理称为**曲面的唯一性定理**，在理论上有十分重要的意义，以后我们还要给出它的一些应用。要判断采用不同参数系的两个曲面在空间$$\mathbb{E}^3$$的一个刚体运动下是否能够重合，综合[定理3.4](/2023/10/18/DifferentialGeometry-NOTES-03.html#正则参数曲面之间的对应)和这里的曲面唯一性定理，我们有下面的结论。

**定理5.2** 设$$S_1$$、$$S_2$$是空间$$\mathbb{E}^3$$的两个正则参数曲面，其第一基本形式和第二基本形式分别是$$\mathrm{I}_i$$和$$\mathrm{II}_i$$。如果有光滑映射$$\sigma: S_1 \rightarrow S_2$$，使得$$\sigma^* \mathrm{I}_2 = \mathrm{I}_1$$且$$\sigma^* \mathrm{II}_2 = \mathrm{II}_1$$，则曲面$$S_1$$、$$S_2$$经过$$\mathbb{E}^3$$的一个刚体运动是彼此重合的。
{:.info}

## 曲面论基本方程

## 曲面的存在性定理

## Gauss定理
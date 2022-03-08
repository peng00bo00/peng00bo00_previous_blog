---
layout: article
title: OMSCS-SIM课程笔记07-Random Variate Generation
tags: ["OMSCS", "ISYE6644-SIM"]
key: OMSCS-SIM-07
aside:
  toc: true
sidebar:
  nav: OMSCS-SIM
---

> 这个系列是Gatech OMSCS 仿真和建模课程([ISYE 6644: Simulation and Modeling for Engineering and Science](https://omscs.gatech.edu/isye-6644-simulation-and-modeling-engineering-and-science))的同步课程笔记。课程内容涉及计算机模拟在统计分析和建模中的应用，本节介绍常用的随机变量生成方法。
<!--more-->

利用均匀分布U(0, 1)我们可以构造出各种不同类型的随机变量。

<div align=center>
<img src="https://i.imgur.com/FgpAKEH.png" width="80%">
</div>

## Inverse Transform Method

最基本的随机变量生成算法是**逆变换方法(inverse transform method)**，它的理论基础是**逆变换定理(inverse transform theorem)**：对于任意连续型随机变量$X$，把CDF作用在$X$上会得到均匀分布U(0, 1)。

<div align=center>
<img src="https://i.imgur.com/KSJ0H5A.png" width="80%">
<img src="https://i.imgur.com/9sEWTO8.png" width="80%">
</div>

要使用逆变换方法进行采样只需要从均匀分布中采样一个随机数$U$，然后利用CDF的反函数即可$X = F^{-1}(U)$。

<div align=center>
<img src="https://i.imgur.com/1f8kK7N.png" width="80%">
</div>

### Continuous Examples

很多常见分布的CDF都具有比较简单的解析形式，因此我们可以使用逆变换方法来生成来自这些分布的随机数。

<div align=center>
<img src="https://i.imgur.com/AGkD6WP.png" width="80%">
<img src="https://i.imgur.com/r0RmonG.png" width="80%">
<img src="https://i.imgur.com/w0xgHBh.png" width="80%">
</div>

但需要注意的是，正态分布的CDF是不具有解析形式的。如果一定要使用逆变换方法生成正态分布的随机数则可以通过一些近似方法来近似标准正态分布的CDF。

<div align=center>
<img src="https://i.imgur.com/XggONpi.png" width="80%">
<img src="https://i.imgur.com/pbtiPO3.png" width="80%">
</div>

得到标准正态分布的随机数后只要通过简单变形就可以获得其它均值和方差所定义的正态分布。

<div align=center>
<img src="https://i.imgur.com/mdzV34T.png" width="80%">
</div>

### Discrete Examples

对于离散型随机变量，可以把CDF转换成一个分段函数然后利用逆变换方法来进行采样。

<div align=center>
<img src="https://i.imgur.com/RDUVgEF.png" width="80%">
<img src="https://i.imgur.com/R5Cv7FR.png" width="80%">
</div>

对于几何分布Geom($p$)则可以通过取整函数来辅助进行采样：

<div align=center>
<img src="https://i.imgur.com/LtMQYFj.png" width="80%">
</div>

不过更常用的方法是利用几何分布和Bernoulli分布的关系来进行采样。

<div align=center>
<img src="https://i.imgur.com/EJRrLAq.png" width="80%">
</div>

而对于Poisson分布Pois($\lambda$)则可以根据需要动态拓展CDF表格，直到随机数落在指定的区间上。

<div align=center>
<img src="https://i.imgur.com/PA6dxAi.png" width="80%">
<img src="https://i.imgur.com/EQmrEUC.png" width="80%">
</div>

### Empirical Distributions

在很多情况下我们无法使用已知的分布来表示随机变量，此时可以利用**经验分布(empirical distributions)**来近似它的CDF。

<div align=center>
<img src="https://i.imgur.com/bIoV68A.png" width="80%">
</div>

得到均匀分布随机数$U$后可以在对应的区间上进行线性插值生成所需的随机数。

<div align=center>
<img src="https://i.imgur.com/2RPNuQ9.png" width="80%">
</div>

## Cutpoint Method

## Convolution Method

这里**卷积(convolution)**是指把随机变量加起来构造新的随机变量。比如说二项分布Bin($n$, $p$)可以看做是$n$个参数为$p$的Bernoulli分布之和。

<div align=center>
<img src="https://i.imgur.com/Sstcadj.png" width="80%">
</div>

类似地，三角分布Triangular(0, 1, 2)等于两个均匀分布U(0, 1)的和。

<div align=center>
<img src="https://i.imgur.com/4cimUqd.png" width="80%">
</div>

Erlang分布则是指数分布的和。

<div align=center>
<img src="https://i.imgur.com/nUyqVFC.png" width="80%">
</div>

根据CLT我们还可以利用大量的均匀分布来构造出标准正态分布。

<div align=center>
<img src="https://i.imgur.com/AZGPBYL.png" width="80%">
</div>

使用卷积来构造的其它常用分布如下：

<div align=center>
<img src="https://i.imgur.com/qm0ERsu.png" width="80%">
</div>

## Acceptance-Rejection Method

为了解决随机变量CDF无法计算的问题人们还开发出了**接受-拒绝方法(acceptance-rejection method)**来进行采样。接受-拒绝方法的思想是首先从一个已知的分布进行采样，如果生成的样本满足要求就接受它。

<div align=center>
<img src="https://i.imgur.com/v5BJhuj.png" width="80%">
</div>

接受-拒绝方法严格的定义如下：设我们想要采样的PDF为$f(x)$，已知的PDF为$h(x)=\frac{t(x)}{c}$，且它们满足

$$
t(x) \geq f(x)
$$

我们从$h(x)$采样一个样本$Y$，同时从均匀分布采样一个样本$U$。如果$U$满足

$$
U \leq \frac{f(Y)}{t(Y)}
$$

则接受样本$Y$，且认为$Y$来自于分布$f(y)$。

<div align=center>
<img src="https://i.imgur.com/n97MFdO.png" width="80%">
<img src="https://i.imgur.com/00zpMHQ.png" width="80%">
<img src="https://i.imgur.com/TGx62UA.png" width="80%">
</div>

### Proof

接下来我们证明一下接受-拒绝方法的正确性。记事件$A$为接受样本$Y$，那么按照接受-拒绝方法得到的样本具有CDF：

$$
P(X \leq x) = P(Y \leq x \vert A) = \frac{P(A, Y \leq x)}{P(A)}
$$

而对于事件$A$则有：

$$
\begin{aligned}
P(A \vert Y = y) &= P(U \leq g(Y) \vert Y = y) \\
&= P(U \leq g(y) \vert Y = y) \\
&= P(U \leq g(y)) \\
&= g(y)
\end{aligned}
$$

利用全概率公式可以得到联合概率：

$$
\begin{aligned}
P(A, Y \leq x) &= \int_{-\infty}^\infty P(A, Y \leq x \vert Y = y) h(y) \ dy \\
&= \int_{-\infty}^x P(A \vert Y = y) h(y) \ dy \\
&= \frac{1}{c} \int_{-\infty}^x P(A \vert Y = y) t(y) \ dy \\
&= \frac{1}{c} \int_{-\infty}^x g(y) t(y) \ dy \\
&= \frac{1}{c} \int_{-\infty}^x f(y) \ dy
\end{aligned}
$$

令$x \to \infty$可以得到：

$$
P(A) = \frac{1}{c} \int_{-\infty}^\infty f(y) \ dy = \frac{1}{c}
$$

把上面的这些式子带入CDF有：

$$
P(X \leq x) = \frac{P(A, Y \leq x)}{P(A)} = \int_{-\infty}^x f(y) \ dy
$$

因此$X$的PDF即为$f(x)$：

$$
\frac{d P(X \leq x)}{dx} = \frac{d}{dx} \int_{-\infty}^x f(y) \ dy = f(x)
$$

<div align=center>
<img src="https://i.imgur.com/q8zPyLo.png" width="80%">
<img src="https://i.imgur.com/Yr1tzb9.png" width="80%">
<img src="https://i.imgur.com/8K0NvPu.png" width="80%">
</div>

### Continuous Examples

在使用接受-拒绝方法进行采样时一般要求已知分布$h(y)$可以进行快速的采样，同时常数$c$需要尽可能接近1，这样可以保证不会拒绝掉太多的样本。

<div align=center>
<img src="https://i.imgur.com/cLPUtVc.png" width="80%">
</div>

对于CDF不可逆的函数我们无法使用逆变换方法进行采样，此时仍然可以使用接受-拒绝方法：

<div align=center>
<img src="https://i.imgur.com/IKD0SPg.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/AFRfc74.png" width="80%">
</div>

### Poisson Distribution

接受-拒绝方法的经典应用是生成Poisson分布的随机数，这里介绍一种接受-拒绝方法的变体。根据定义，Poisson分布的样本可以理解为计数过程单位时间内的到达数量，参数$\lambda$为单位时间内的平均到达数量。

<div align=center>
<img src="https://i.imgur.com/VMuDFMM.png" width="80%">
</div>

因此可以利用计数过程来生成Poisson分布的随机数。同时注意到相邻到达的时间间隔服从指数分布Exp($\lambda$)，这样就可以利用指数分布的随机数序列来模拟计数过程。

<div align=center>
<img src="https://i.imgur.com/BmaBBg8.png" width="80%">
</div>

上面的推导说明我们只需要从均匀分布中采样出一个随机数序列，选择它们累乘恰好小于$e^{-\lambda}$时的序数即为来自Poisson分布的样本。

<div align=center>
<img src="https://i.imgur.com/FklndIq.png" width="80%">
<img src="https://i.imgur.com/Hk4F1dO.png" width="80%">
</div>

对于参数$\lambda$比较大的情况还可以利用正态分布的随机数来近似Poisson分布。

<div align=center>
<img src="https://i.imgur.com/EpGjC8w.png" width="80%">
<img src="https://i.imgur.com/wFzb7WD.png" width="80%">
</div>

## Composition Method

## Special-Case Techniques

## Multivariate Normal Distribution

## Generating Stochastic Process

## Reference

- [Random Variate Generation](https://www2.isye.gatech.edu/~sman/courses/6644/Module07-RandomVariateGenerationSlides-201026.pdf)
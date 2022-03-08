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

利用CLT我们还可以构造出标准正态分布。

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

### Continuous Examples

## Composition Method

## Special-Case Techniques

## Multivariate Normal Distribution

## Generating Stochastic Process

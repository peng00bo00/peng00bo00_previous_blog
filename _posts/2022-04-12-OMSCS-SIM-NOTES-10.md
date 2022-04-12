---
layout: article
title: OMSCS-SIM课程笔记10-Comparing Systems
tags: ["OMSCS", "ISYE6644-SIM"]
key: OMSCS-SIM-10
aside:
  toc: true
sidebar:
  nav: OMSCS-SIM
---

> 这个系列是Gatech OMSCS 仿真和建模课程([ISYE 6644: Simulation and Modeling for Engineering and Science](https://omscs.gatech.edu/isye-6644-simulation-and-modeling-engineering-and-science))的同步课程笔记。课程内容涉及计算机模拟在统计分析和建模中的应用，本节介绍利用随机模拟的结果对系统进行对比和评价的方法。
<!--more-->

## Introduction and Review of Classical Confidence Intervals

**置信区间(confidence intervals, CI)**是系统评价最常用的方法，因此我们首先来回顾一下CI的概念和性质。

<div align=center>
<img src="https://i.imgur.com/EumBLyk.png" width="80%">
</div>

### Confidence Intervals for the Mean

假设有一系列独立同分布的正态分布随机变量$\{ X_i \}$，我们可以计算它们的样本均值$\bar{X}_n$和方差$S_X^2$。在此基础上，我们构造统计量$T$：

$$
T = \frac{\bar{X}_n - \mu}{\sqrt{S_X^2 / n}} = \frac{\frac{\bar{X}_n - \mu}{\sqrt{\sigma^2 / n}}}{\sqrt{S_X^2 / \sigma^2}}
$$

可以证明统计量$T$服从参数为$n-1$的$t$分布，$T \sim t(n-1)$。

<div align=center>
<img src="https://i.imgur.com/8N1fMJu.png" width="80%">
<img src="https://i.imgur.com/kbIHPDX.png" width="80%">
</div>

利用统计量$T$可以得到总体方差$\sigma^2$未知条件下样本均值的置信区间：

<div align=center>
<img src="https://i.imgur.com/b2WhMJY.png" width="80%">
</div>

### Confidence Intervals Difference Two Means

接下来考虑样本来自两个正态分布的情况。假设$\{ X_i \}$来自正态分布$N(\mu_X, \sigma_X^2)$，$\{ Y_i \}$来自$N(\mu_Y, \sigma_Y^2)$，根据我们已知的信息可以构造出不同的置信区间。

<div align=center>
<img src="https://i.imgur.com/VBrJuRQ.png" width="80%">
</div>

如果$\{ X_i \}$和$\{ Y_i \}$有着相同但是未知的方差，可以构造出它们均值差异的置信区间为：

<div align=center>
<img src="https://i.imgur.com/Gn8UV4V.png" width="80%">
</div>

如果$\{ X_i \}$和$\{ Y_i \}$有着不相同的方差，可以构造出它们均值差异的置信区间为：

<div align=center>
<img src="https://i.imgur.com/oyENHzR.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/lF1CvDR.png" width="80%">
<img src="https://i.imgur.com/PoSROpM.png" width="80%">
</div>

### Paired CI Difference Two Means

现实中另一种常见的情况是$\{ X_i \}$和$\{ Y_i \}$自身满足独立同分布，但每一对$(X_i, Y_i)$则存在相互关联。

<div align=center>
<img src="https://i.imgur.com/GEHZFIb.png" width="80%">
<img src="https://i.imgur.com/ToB43Cj.png" width="80%">
</div>

在这种情况下可以构造出差异$D$的置信区间：

<div align=center>
<img src="https://i.imgur.com/ImQXF8T.png" width="80%">
<img src="https://i.imgur.com/qnjKNtY.png" width="80%">
<img src="https://i.imgur.com/s2y3hOT.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/YWzkXPM.png" width="80%">
<img src="https://i.imgur.com/lgPM2VU.png" width="80%">
</div>

## Comparison of Simulated Systems

在随机模拟中数据之间往往不满足独立同分布假设，在这种情况下我们需要一些额外的处理来推导出置信区间。

<div align=center>
<img src="https://i.imgur.com/U0KJPLl.png" width="80%">
<img src="https://i.imgur.com/PAy7qws.png" width="80%">
</div>

### Confidence Intervals for Mean Differences

利用独立重复试验，我们可以估计两个系统自身的均值和方差：

<div align=center>
<img src="https://i.imgur.com/cLoKVKK.png" width="80%">
</div>

得到均值和方差后就可以计算两个系统差异的置信区间：

<div align=center>
<img src="https://i.imgur.com/rWSWTo3.png" width="80%">
</div>

另一种可行的策略是把两个系统的试验看成是一对，然后利用[Paired CI Difference](#paired-ci-difference-two-means)的方法来估计置信区间：

<div align=center>
<img src="https://i.imgur.com/UPcwkd5.png" width="80%">
</div>

### Variance Reduction Techniques

## Ranking and Selection Methods

## Reference

- [Comparing Systems](https://www2.isye.gatech.edu/~sman/courses/6644/Module10-ComparingSystems-201128.pdf)
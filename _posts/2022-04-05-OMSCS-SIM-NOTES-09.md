---
layout: article
title: OMSCS-SIM课程笔记09-Output Analysis
tags: ["OMSCS", "ISYE6644-SIM"]
key: OMSCS-SIM-09
aside:
  toc: true
sidebar:
  nav: OMSCS-SIM
---

> 这个系列是Gatech OMSCS 仿真和建模课程([ISYE 6644: Simulation and Modeling for Engineering and Science](https://omscs.gatech.edu/isye-6644-simulation-and-modeling-engineering-and-science))的同步课程笔记。课程内容涉及计算机模拟在统计分析和建模中的应用，本节介绍对随机模拟的输出结果进行分析的方法。
<!--more-->

## Introduction

回忆进行仿真的流程，当我们完成了试验设计并且进行了模拟后就需要对收集到的数据进行分析。

<div align=center>
<img src="https://i.imgur.com/8VIDnKq.png" width="80%">
</div>

对输出结果进行分析的原因之一在于我们在进行模拟时的输入是随机的，因此系统的输出也必然是随机变量。这样就需要考虑采样误差对于系统输出结果的影响。

<div align=center>
<img src="https://i.imgur.com/ig99nEc.png" width="80%">
</div>

对随机输出结果进行分析的常用指标包括均值、方差、分位数等，同时我们也会使用点估计或是置信区间的方法来进行分析。

<div align=center>
<img src="https://i.imgur.com/PGfzLvg.png" width="80%">
</div>

输出结果分析的难点在于样本之间往往是不满足独立同分布假定的。以排队问题为例，相邻用户之间的等待时间显然是相互关联的。在这种情况下之间套用一些常用的估计方法会导致额外偏差。

<div align=center>
<img src="https://i.imgur.com/t3ME1kT.png" width="80%">
<img src="https://i.imgur.com/GyPIrFg.png" width="80%">
</div>

总之，我们在对仿真结果进行分析时需要考虑样本之间的相互影响。直接使用经典统计分析的方法可能是不合适的。

<div align=center>
<img src="https://i.imgur.com/0mjwa9M.png" width="80%">
</div>

在本节课中我们将主要介绍两种分析方法：其一是**finite-horizon simulation**，它比较适合分析系统短期的行为；另一种是**steady-state analysis**，它则更关注系统的长期行为。

<div align=center>
<img src="https://i.imgur.com/X2aDH6w.png" width="80%">
<img src="https://i.imgur.com/YoqZ0bI.png" width="80%">
</div>

## A Mathematical Interlude

在正式介绍具体的结果分析方法前我们首先来看一下当样本之间存在相关性时会产生什么样的问题。这里我们假设样本具有相同的分布，但并不是相互独立的。

<div align=center>
<img src="https://i.imgur.com/MvYpTwQ.png" width="80%">
</div>

在这种情况下样本均值$E[\bar{Y}_n]$仍然等于分布的均值$\mu$，我们考虑它的方差可以得到如下公式：

<div align=center>
<img src="https://i.imgur.com/Wyqf0sE.png" width="80%">
<img src="https://i.imgur.com/SNOxW1V.png" width="80%">
<img src="https://i.imgur.com/0u5zuCq.png" width="80%">
</div>

当样本之间相互独立时，参数$\sigma^2$恰好等于分布的方差。但在样本之间相互关联的情况下$\sigma^2$往往会远大于真实的方差，这会导致在计算置信区间时产生非常大的误差。

<div align=center>
<img src="https://i.imgur.com/FeXCHqh.png" width="80%">
</div>

举一个具体的例子，我们假设样本由自回归过程产生。在这种条件下样本的均值会有非常巨大的方差。

<div align=center>
<img src="https://i.imgur.com/FyAJqeS.png" width="80%">
</div>

当我们使用样本均值对分布的其它参数进行估计时，样本之间的相关性同样会产生巨大的影响。以样本方差为例，如果我们直接套用独立同分布条件下的样本方差公式则会导致样本方差的期望远小于样本均值的方差。

<div align=center>
<img src="https://i.imgur.com/QqHoGcs.png" width="80%">
<img src="https://i.imgur.com/bmtWNc9.png" width="80%">
<img src="https://i.imgur.com/0fEj2DA.png" width="80%">
</div>

如果错误地使用了样本方差公式则会计算出远小于真实情况下的置信区间。

<div align=center>
<img src="https://i.imgur.com/exreS2E.png" width="80%">
</div>

## Finite-Horizon Simulation

### Finite-Horizon Analysis

finite-horizon simulation的目的是确定系统在相对短期内的行为。

<div align=center>
<img src="https://i.imgur.com/SV3I1g4.png" width="80%">
<img src="https://i.imgur.com/wTpPJY2.png" width="80%">
</div>

其中，最简单的任务是使用样本均值来估计观测的结果。但需要注意的是由于样本之间不是独立同分布的，我们不能直接使用样本方差来来估计总体的方差。

<div align=center>
<img src="https://i.imgur.com/R0VTudP.png" width="80%">
<img src="https://i.imgur.com/ZZgxjwJ.png" width="80%">
</div>

要解决这个问题也很简单，我们只需要进行**独立重复试验(independent replications, IR)**即可。

<div align=center>
<img src="https://i.imgur.com/QFZXu1I.png" width="80%">
</div>

通过独立重复试验，我们可以得到满足独立同分布假定的观测均值$Z_i$，此时就可以使用标准的参数估计方法来估计总体方差了。

<div align=center>
<img src="https://i.imgur.com/URqJmm4.png" width="80%">
<img src="https://i.imgur.com/JY6uHPN.png" width="80%">
</div>

当每次试验中的观测数足够大时我们还可以使用中心极限定理来估计均值的置信区间。

<div align=center>
<img src="https://i.imgur.com/34nb4sJ.png" width="80%">
</div>

### Finite-Horizon Extensions

在独立重复试验的基础上如果想要得到一个更紧的置信区间则可以考虑增加试验的次数。可以证明区间的半径与试验次数成平方反比关系，换句话说如果想要把区间半径减小一半需要4倍次数的试验。

<div align=center>
<img src="https://i.imgur.com/j5202pb.png" width="80%">
</div>

另一方面，我们还可以去估计均值以外其它统计量的置信区间。以分位数为例，我们可以推导出分位数的置信区间如下：

<div align=center>
<img src="https://i.imgur.com/hRJR82X.png" width="80%">
<img src="https://i.imgur.com/Qipo6XC.png" width="80%">
<img src="https://i.imgur.com/4ohSGjj.png" width="80%">
<img src="https://i.imgur.com/HWFpkmT.png" width="80%">
<img src="https://i.imgur.com/cWd4uj6.png" width="80%">
<img src="https://i.imgur.com/Nj3SuEq.png" width="80%">
</div>

## Initialization Problems

## Steady-State Analysis

## Reference

- [Output Analysis](https://studio.edx.org/assets/courseware/v1/ddb0b74e23388195b0ac265c61c7c3c7/asset-v1:GTx+ISYE6644x+2T2019+type@asset+block/Module09-OutputAnalysis_171019.pdf)
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

## Finite-Horizon Simulation

## Initialization Problems

## Steady-State Analysis

## Reference

- [Output Analysis](https://studio.edx.org/assets/courseware/v1/ddb0b74e23388195b0ac265c61c7c3c7/asset-v1:GTx+ISYE6644x+2T2019+type@asset+block/Module09-OutputAnalysis_171019.pdf)
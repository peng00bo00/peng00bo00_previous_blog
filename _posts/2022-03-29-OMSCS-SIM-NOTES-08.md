---
layout: article
title: OMSCS-SIM课程笔记08-Input Analysis
tags: ["OMSCS", "ISYE6644-SIM"]
key: OMSCS-SIM-08
aside:
  toc: true
sidebar:
  nav: OMSCS-SIM
---

> 这个系列是Gatech OMSCS 仿真和建模课程([ISYE 6644: Simulation and Modeling for Engineering and Science](https://omscs.gatech.edu/isye-6644-simulation-and-modeling-engineering-and-science))的同步课程笔记。课程内容涉及计算机模拟在统计分析和建模中的应用，本节介绍对随机模拟的输入进行分析的方法。
<!--more-->

## Intro to Input Analysis

到目前为止我们已经介绍过如何进行随机模拟以及如何生成各种类型的随机变量，但进行具体的模拟前我们还需要判断该选择什么类型的随机变量进行模拟，确定使用随机变量的过程称为**输入分析(input analysis)**。

<div align=center>
<img src="https://i.imgur.com/7yRA8U7.png" width="80%">
<img src="https://i.imgur.com/tTfPT1l.png" width="80%">
</div>

显然输入分析对于随机模拟非常重要，它的基本流程包括收集数据、估计随机变量的分布以及验证概率分布是否符合收集到的数据。

<div align=center>
<img src="https://i.imgur.com/MjUJW0l.png" width="80%">
</div>

**直方图(histogram)**是输入分析最基本的方法，利用直方图我们可以直观地显示随机变量的分布情况。实际上当收集到的数据足够多时，直方图会收敛到数据真实分布的PDF上。

<div align=center>
<img src="https://i.imgur.com/CzihpnL.png" width="80%">
</div>

**茎叶图(stem-and-leaf diagram)**是输入分析的另一种常用方法，它可以看做是直方图的一个变种。

<div align=center>
<img src="https://i.imgur.com/irEXgj9.png" width="80%">
</div>

在确定随机变量的分布时需要思考随机变量是离散变量还是连续变量、是一维变量还是多维变量等等。

<div align=center>
<img src="https://i.imgur.com/oGO5FJD.png" width="80%">
</div>

常用随机变量分布的应用场景如下：

<div align=center>
<img src="https://i.imgur.com/4EElTCW.png" width="80%">
<img src="https://i.imgur.com/qR8CV1h.png" width="80%">
</div>

总结一下，输入分析的基本思路是根据收集到的数据来选择一个概率分布，然后利用一些统计检验来验证我们的选择时合理的。

<div align=center>
<img src="https://i.imgur.com/Qz1HxXF.png" width="80%">
</div>

## Point Estimation

### Intro to Estimation

### Unbiased Estimation

### Mean Squared Error

### Maximum Likelihood Estimation

### Method of Moments

## Goodness-of-Fit Tests

## Reference

- [Input Analysis](https://www2.isye.gatech.edu/~sman/courses/6644/Module08-InputAnalysis-210814.pdf)
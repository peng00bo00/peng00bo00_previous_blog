---
layout: article
title: OMSCS-SIM课程笔记06-Random Number Generation
tags: ["OMSCS", "ISYE6644-SIM"]
key: OMSCS-SIM-06
aside:
  toc: true
sidebar:
  nav: OMSCS-SIM
---

> 这个系列是Gatech OMSCS 仿真和建模课程([ISYE 6644: Simulation and Modeling for Engineering and Science](https://omscs.gatech.edu/isye-6644-simulation-and-modeling-engineering-and-science))的同步课程笔记。课程内容涉及计算机模拟在统计分析和建模中的应用，本节介绍常用的随机数生成方法。
<!--more-->

生成(0, 1)区间上的均匀分布随机数是各种随机模拟技术的基础，利用Uniform(0,1)可以构造出各种不同类型的随机变量。因此随机数生成算法的目标是产生一个伪随机数序列且它们服从相互独立的均匀分布。

<div align=center>
<img src="https://i.imgur.com/zYV9bH4.png" width="80%">
</div>

## Some lousy generators

早期的随机数生成算法是基于物理过程来产生真实的随机数，这类方法产生的结果有很好的随机性但几乎无法进行重复试验。在此基础上人们还整理了随机数表格然后通过查表的方式来产生可复现的随机数。

<div align=center>
<img src="https://i.imgur.com/4zHNcm9.png" width="80%">
</div>

后来von Neumann发明了**平方取中法(mid-square method)**来生成随机数，然而这种方法生成的随机数效果并不好。

<div align=center>
<img src="https://i.imgur.com/fO6ZTxP.png" width="80%">
</div>

人们还发明了**加同余法(additive congruential method)**来生成随机数，但它同样具有一些问题。

<div align=center>
<img src="https://i.imgur.com/RnzAqxm.png" width="80%">
</div>

## Linear Congruential Generators

前面介绍的这些随机数生成算法现在已经弃用，目前最常用的算法是**线性同余法(linear congruential generator, LCG)**。LCG的一个缺陷在于它会产生循环出现的随机数，因此在选择参数时要额外小心。

<div align=center>
<img src="https://i.imgur.com/WUHPKKY.png" width="80%">
<img src="https://i.imgur.com/UcAMLJJ.png" width="80%">
<img src="https://i.imgur.com/LWJKrZp.png" width="80%">
<img src="https://i.imgur.com/yxP7QHi.png" width="80%">
</div>

## Tausworthe Generator

除了LCG外目前常用的随机数生成器还包括**Tausworthe生成器(Tausworthe generator)**。Tausworthe生成器定义了一个比特序列$B_i$，它通过位运算来生成新的比特。

<div align=center>
<img src="https://i.imgur.com/fUsCb5m.png" width="80%">
<img src="https://i.imgur.com/WoaYgk8.png" width="80%">
</div>

要获得随机数只需要先将比特序列视为二进制数，再转换成小数即可。

<div align=center>
<img src="https://i.imgur.com/mssmCig.png" width="80%">
</div>

## Generalizations of LCGs

在实际使用LCG时一般会进行一些拓展，最常用的拓展方法是将线性变换推广成向量乘法，即每次取前$q$次的结果来计算新的随机数。

<div align=center>
<img src="https://i.imgur.com/AKylKQm.png" width="80%">
</div>

另一种常用的拓展方法是将两个LCG组合起来形成一个新的随机数生成器。

<div align=center>
<img src="https://i.imgur.com/uOJgFOJ.png" width="80%">
<img src="https://i.imgur.com/E3eJG9J.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/5pFxexT.png" width="80%">
</div>

## Choosing a Good Generator

### Some Theory

关于LCG还有很多理论上的性质，这些性质证明起来比较复杂这里直接介绍相关的结论。

<div align=center>
<img src="https://i.imgur.com/hhHHnjz.png" width="80%">
<img src="https://i.imgur.com/tmwrFpS.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/UHgwC7v.png" width="80%">
<img src="https://i.imgur.com/5z087un.png" width="80%">
</div>

### Statistical Tests

## Reference

- [Random Number Generation](https://www2.isye.gatech.edu/~sman/courses/6644/Module06-RandomNumberGenerationSlides-200322.pdf)
---
layout: article
title: OMSCS-GA课程笔记02-Divide and Conquer
tags: ["OMSCS", "CS6515-GA"]
key: OMSCS-GA-02
aside:
  toc: true
sidebar:
  nav: OMSCS-GA
---

> 这个系列是Gatech OMSCS 高级算法课程([CS 6515: Intro to Grad Algorithms](https://omscs.gatech.edu/cs-6515-intro-graduate-algorithms))的同步课程笔记。课程内容涉及动态规划、随机算法、分治、图算法、最大流、线性规划以及NP完备等高级算法的设计思想和相关应用，本节主要介绍分治。
<!--more-->

**分治(Divide and Conquer)**是算法设计中非常重要的一种思想，很多常用的算法都是基于分治来设计和实现的。

## Fast Integer Multiplication

分治的一个基本应用是计算高位整数的乘法。当数字的位数高到无法直接计算时，我们仍然可以利用分治的思想来进行求解。

<div align=center>
<img src="https://i.imgur.com/bdKavlE.png" width="80%">
</div>

### Gauss's Idea

在大多数情况下数字加减的计算代价是要小于乘除的，因此在进行计算时我们希望尽可能多地减少乘除计算的次数。以复数的乘法为例，两个复数的乘积需要进行4次乘法计算。但通过合理的算法我们可以把乘法计算降低到3次。

<div align=center>
<img src="https://i.imgur.com/GVgFnPp.png" width="80%">
<img src="https://i.imgur.com/sZlpuXw.png" width="80%">
</div>

### Naive Approach

回到高位整数乘法的问题，我们可以把数字拆成两半然后分别求解乘法。这样就可以得到一个递归的算法：

<div align=center>
<img src="https://i.imgur.com/KYNNu2s.png" width="80%">
<img src="https://i.imgur.com/mctTDhl.png" width="80%">
</div>

递归算法的伪代码如下：

```
EasyMultiply(x, y):
    xL = first n/2 bits of x
    xR = last n/2 bits of x
    yL = first n/2 bits of y
    yR = last n/2 bits of y

    A = EasyMultiply(xL, yL)
    B = EasyMultiply(xR, yR)
    C = EasyMultiply(xL, yR)
    D = EasyMultiply(xR, yL)

    z = A << n + (C + D) << (n/2) + B

    return z
```

<div align=center>
<img src="https://i.imgur.com/VXV71gO.png" width="80%">
</div>

利用主定理可以得到`EasyMultiply(x, y)`的复杂度为$O(n^2)$：

$$
T(n) = 4T(n/2) + O(n) = O(n^2)
$$

<div align=center>
<img src="https://i.imgur.com/n58W1jH.png" width="80%">
<img src="https://i.imgur.com/n58W1jH.png" width="80%">
<img src="https://i.imgur.com/lB86OST.png" width="80%">
</div>

### Improved Approach

通过减少递归计算的次数可以降低整个算法的复杂度。具体地，我们利用[复数乘法](/2022/09/06/OMSCS-GA-NOTES-02.html#gausss-idea)的技巧来减少一次递归乘法。

<div align=center>
<img src="https://i.imgur.com/7Jl4b9D.png" width="80%">
</div>

此时的伪代码如下：

```
FastMultiply(x, y):
    xL = first n/2 bits of x
    xR = last n/2 bits of x
    yL = first n/2 bits of y
    yR = last n/2 bits of y

    A = FastMultiply(xL, yL)
    B = FastMultiply(xR, yR)
    C = FastMultiply(xL+xR, yL+yR)

    z = A << n + (C - A - B) << (n/2) + B

    return z
```

<div align=center>
<img src="https://i.imgur.com/EQfdgzn.png" width="80%">
</div>

改进后的计算复杂度为$O(n^{\log_2 3})$：

$$
T(n) = 3T(n/2) + O(n) = O(n^{\log_2 3})
$$

<div align=center>
<img src="https://i.imgur.com/04ipg9c.png" width="80%">
</div>

## Solving Recurrences

分治算法的核心在于构造递归问题。

<div align=center>
<img src="https://i.imgur.com/UPw8X8i.png" width="80%">
</div>

在分析算法复杂度时可以利用几何级数来进行考虑：

<div align=center>
<img src="https://i.imgur.com/uxDGtbz.png" width="80%">
<img src="https://i.imgur.com/2STHrYi.png" width="80%">
<img src="https://i.imgur.com/59tnnSD.png" width="80%">
<img src="https://i.imgur.com/uPej1mc.png" width="80%">
<img src="https://i.imgur.com/AElHcuT.png" width="80%">
</div>

对于更一般的情况，可以利用递归次数以及子问题的规模来分析整个算法的复杂度：

<div align=center>
<img src="https://i.imgur.com/36tW5l5.png" width="80%">
</div>

## FFT

### Polynomial Multiplication

前面我们介绍过高位数字以及矩阵乘法的加速算法，而对于多项式我们使用它的系数来进行表示。此时两个$n-1$次多项式的乘法是一个$2n-2$次多项式，其系数可以使用两个多项式系数的卷积来计算：

<div align=center>
<img src="https://i.imgur.com/21gGrnL.png" width="80%">
</div>

对于更一般的情况，我们定义多项式的乘法为对应系数的卷积。显然可以在$O(n^2)$的时间内来完成计算，但实际上我们可以在$O(n \log (n))$时间内完成卷积。

<div align=center>
<img src="https://i.imgur.com/Y9HQBHd.png" width="80%">
</div>

### Convolution Applications

卷积运算在工程中有着大量的应用，比如说信号处理中的各种滤波器就是使用卷积来定义和实现的。

<div align=center>
<img src="https://i.imgur.com/3TRmA58.png" width="80%">
</div>

### Polynomial Basics

回到多项式的计算，我们可以使用系数来表达多项式也可以使用它在一系列点上的值来进行表示。在数学上可以证明这两种表达形式是相互等价的，而且可以通过FFT来相互转换。

<div align=center>
<img src="https://i.imgur.com/1afFnbL.png" width="80%">
<img src="https://i.imgur.com/9wLnONK.png" width="80%">
</div>

更进一步，通过采样点来表示的多项式更适合进行卷积运算。我们只需要把对应位置上的数值相乘即可：

<div align=center>
<img src="https://i.imgur.com/MfabNoG.png" width="80%">
</div>

### FFT: Opposites

FFT的核心是选择合适的采样点。

<div align=center>
<img src="https://i.imgur.com/Kv0GnQc.png" width="80%">
</div>

## Median

## Reference

- [Divide & Conquer](https://teapowered.dev/assets/ga-notes.pdf#page=22)
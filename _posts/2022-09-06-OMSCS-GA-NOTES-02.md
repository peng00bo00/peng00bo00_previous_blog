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

通过减少递归计算的次数我们降低整个算法的复杂度。具体地，我们利用复数计算的技巧可以减少一次递归乘法。

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

## Complex Numbers

## Reference

- [Divide & Conquer](https://teapowered.dev/assets/ga-notes.pdf#page=22)
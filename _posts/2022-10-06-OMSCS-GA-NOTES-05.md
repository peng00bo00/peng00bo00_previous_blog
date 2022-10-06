---
layout: article
title: OMSCS-GA课程笔记05-Randomized Algorithms
tags: ["OMSCS", "CS6515-GA"]
key: OMSCS-GA-05
aside:
  toc: true
sidebar:
  nav: OMSCS-GA
---

> 这个系列是Gatech OMSCS 高级算法课程([CS 6515: Intro to Grad Algorithms](https://omscs.gatech.edu/cs-6515-intro-graduate-algorithms))的同步课程笔记。课程内容涉及动态规划、随机算法、分治、图算法、最大流、线性规划以及NP完备等高级算法的设计思想和相关应用，本节主要介绍随机算法。
<!--more-->

随机算法是算法中的一个分支，在密码学中随机算法有着非常重要的应用。

<div align=center>
<img src="https://i.imgur.com/kmkXxWQ.png" width="80%">
</div>

## Modular Arithmetic

在介绍随机算法与密码学的关系前我们需要先来引入**模算数(modular arithmetic)**的相关概念。对于整数$x$我们定义取模运算mod来获得余数，如果两个整数$x$和$y$具有相同的余数则称它们**同余(congruence)**：

<div align=center>
<img src="https://i.imgur.com/iW67pbi.png" width="80%">
</div>

以除数3为例，通过取模运算可以定义3个同余等价类。

<div align=center>
<img src="https://i.imgur.com/3t2bEYZ.png" width="80%">
</div>

### Basic Fact

同余的一个基本性质是如果$x$和$y$以及$a$和$b$分别同余等价，则$x+a$和$y+b$同余等价且$xa$和$yb$同余等价。

<div align=center>
<img src="https://i.imgur.com/tyHZnld.png" width="80%">
</div>

### Modular Exp

模算数的一个重要应用是计算指数的余数。对于n-bit整数$x$和$y$，我们可以通过递推的方法来计算$x^y$的余数：

<div align=center>
<img src="https://i.imgur.com/XqsNI54.png" width="80%">
</div>

上述算法的复杂度依赖于$y$的大小。更高效的算法是利用平方运算来减少迭代步骤：

<div align=center>
<img src="https://i.imgur.com/868cAeY.png" width="80%">
<img src="https://i.imgur.com/U0Ke678.png" width="80%">
</div>

### Multiplicative Inverse

我们定义mod运算的逆为满足$x z \equiv 1 \ \text{mod} \ N$的整数，记为$x \equiv z^{-1} \ \text{mod} \ N$。

<div align=center>
<img src="https://i.imgur.com/IRRD5SB.png" width="80%">
</div>

需要注意的是并不是所有的整数都存在逆。

<div align=center>
<img src="https://i.imgur.com/6NXFAxN.png" width="80%">
</div>

实际上当且仅当$x$和$N$的**最大公约数(greatest common divisor, GCD)**为1时才存在逆。

<div align=center>
<img src="https://i.imgur.com/xz4S72s.png" width="80%">
<img src="https://i.imgur.com/2qcnxS8.png" width="80%">
<img src="https://i.imgur.com/pb7nmZX.png" width="80%">
<img src="https://i.imgur.com/FKeZrQs.png" width="80%">
</div>

### GCD

因此计算mod的逆就归结于计算$x$和$N$的最大公约数。关于最大公约数的研究可以追溯到古希腊的欧几里得，他指出$x$和$y$的最大公约数等于$(x \ \text{mod} \ y)$和$y$的最大公约数：

<div align=center>
<img src="https://i.imgur.com/XxbUICn.png" width="80%">
</div>

基于欧几里得定理可以得到计算最大公约数的算法，其复杂度为$O(n^3)$：

```
Euclid(x, y):
    if y == 0:
        return x
    
    else:
        return Euclid(y, x mod y)
```

<div align=center>
<img src="https://i.imgur.com/G7LIc8L.png" width="80%">
<img src="https://i.imgur.com/jz8iOIA.png" width="80%">
</div>

## RSA

## Bloom Filters

## Reference

- [Cryptography](https://teapowered.dev/assets/ga-notes.pdf#page=60)
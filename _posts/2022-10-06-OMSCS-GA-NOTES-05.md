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

随机算法在密码学中有着非常重要的应用。

<div align=center>
<img src="https://i.imgur.com/kmkXxWQ.png" width="80%">
</div>

## Modular Arithmetic

在介绍随机算法与密码学的关系前我们需要先来引入**模算数(modular arithmetic)**的相关概念。对于整数$x$我们定义取模运算mod来获得余数，如果两个整数$x$和$y$具有相同的余数则称它们关于$N$**同余(congruence)**：

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

这样就可以计算mod的逆，其复杂度为$O(n^3)：

```
Ext-Euclid(x, y):
  if y == 0:
    return (x, 1, 0)

  else:
    d, alpha', beta' = Ext-Euclid(y, x mod y)
    return (d, beta', alpha' - x//y * beta')
```

<div align=center>
<img src="https://i.imgur.com/hDVaWBu.png" width="80%">
<img src="https://i.imgur.com/B5jfvC0.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/rLqq2wk.png" width="80%">
</div>

## RSA

### Fermat's Little Theorem

在模算数的基础上就可以介绍密码学中重要的RSA算法了，不过在此之前我们还需要引入**费马小定理(Fermat's little theorem)**。它指出对于任意质数$p$和小于$p$的整数$z$，$z^{p-1}$与1关于$p$同余：

<div align=center>
<img src="https://i.imgur.com/B4n9HY4.png" width="80%">
<img src="https://i.imgur.com/k2cdrfL.png" width="80%">
<img src="https://i.imgur.com/BleDVXl.png" width="80%">
<img src="https://i.imgur.com/QeWnBr4.png" width="80%">
</div>

### Euler's Theorem

**欧拉定理(Euler's theorem)**是对费马小定理的推广，它指出互质的整数$N$和$z$，$z^{\phi(N)}$与1关于$N$同余，其中$\phi(N)$为小于$N$且与$N$互质的整数数量。

<div align=center>
<img src="https://i.imgur.com/o5rJuW0.png" width="80%">
</div>

如果我们进一步令$N$为两个质数$p$和$q$的积，可以证明$\phi(N)=(p-1)(q-1)$。这样有$z^{(p-1)(q-1)}$与1关于$N=pq$同余。

<div align=center>
<img src="https://i.imgur.com/0uTjBuG.png" width="80%">
<img src="https://i.imgur.com/ay1HGWH.png" width="80%">
</div>

### RSA Idea

RSA算法的基本思想是利用欧拉定理来对$z$进行加密。我们取两个质数$p$和$q$并计算它们的积$N=pq$，接下来取关于$(p-1)(q-1)$互逆的一对整数$d$和$e$。进行加密时加密方已知$e$和$N$，这样可以计算$z^d$；而在解密时解密方知道$p$、$q$和$e$，利用$z^{de}$就可以恢复$z$。

<div align=center>
<img src="https://i.imgur.com/TnrHrn4.png" width="80%">
</div>

### Cryptography Setting

在密码学中最常见的一类场景是**公开密钥加密(public-key cryptography)**。此时数据发送方通过加密函数`e()`对信息进行加密，而接收方通过解密函数`d()`进行解密，它们之间的直接通信都是加密后的消息`e(m)`。同时接收方会公开**公钥(public key)**，这样任何拥有公钥的人都可以加密，但只有数据接收方能够利用**私钥(private key)**进行解密。

<div align=center>
<img src="https://i.imgur.com/zFEjFeV.png" width="80%">
</div>

### RSA Protocols

因此数据接收方的任务在于计算公钥和私钥，然后公开公钥并保留私钥用来解密。为此它需要首先选择两个质数$p$和$q$，然后计算与$(p-1)(q-1)$互质的$e$用来加密，这样就得到了公钥$N=pq$和$e$，最后计算并保存私钥$d$即可。

<div align=center>
<img src="https://i.imgur.com/vETQhFj.png" width="80%">
</div>

对于数据发送方来说，它只需要先获取公钥$N=pq$和$e$，然后对消息$m$进行加密$y \equiv m^e \ \text{mod} \ N$，最后发送加密后的消息$y$即可。

<div align=center>
<img src="https://i.imgur.com/yIhMZXk.png" width="80%">
</div>

而当接收方需要进行解密时只需要利用私钥计算$y^d \ \text{mod} \ N = m$。

<div align=center>
<img src="https://i.imgur.com/b2tkQab.png" width="80%">
</div>

### RSA Pitfalls

使用RSA进行加密时需要注意的是保证原始数据$m$和$N=pq$是互质的，而如果它们存在公约数则容易导致一些问题。假设$m$和$N$存在公约数$p$，对于数据接收方仍然可以正确地进行解密，但是任何截获加密数据$m^e$的人都可以利用gcd来破解$p$进而获得私钥。因此在进行加密时需要注意验证$m$和$N$是否是互质的。

<div align=center>
<img src="https://i.imgur.com/7QG9xgr.png" width="80%">
</div>

另一方面我们还希望原始数据$m$既不是特别大也不是特别小的数字，当$m$特别大或者特别小时都容易导致加密失效。

<div align=center>
<img src="https://i.imgur.com/9cvB5ys.png" width="80%">
</div>

### RSA Recap

总结一下目前为止的内容，整个RSA算法的流程如下：

<div align=center>
<img src="https://i.imgur.com/IexyKKP.png" width="80%">
<img src="https://i.imgur.com/JcmiC8Z.png" width="80%">
</div>

### Random Prime Numbers

整个RSA算法依赖于选取质数$p$和$q$，因此我们需要设计随机质数的生成算法。要生成随机质数我们首先需要生成随机n-bit整数，整个过程比较简单只需要对n-bit随机赋予0或者1即可。然后我们验证这个随机整数是否是一个质数，如果是质数就得到了一个随机质数，否则重新生成一个新的随机整数再进行判断即可。可以证明n-bit随机整数恰为质数的概率约为$\frac{1}{n}$，因此理论上我们只需要重复生成n次随机整数就可以得到一个随机质数。

<div align=center>
<img src="https://i.imgur.com/lIzdCbC.png" width="80%">
</div>

要验证一个整数是否是质数则需要**费马素性检验(Fermat primality test)**。根据费马小定理，任意小于质数$r$的整数$z$一定有$z^{r-1} \equiv 1 \ \text{mod} \ r$。因此如果我们能够找到一个小于$r$的整数$z$使得$z^{r-1} \not\equiv 1 \ \text{mod} \ r$，那么$r$一定是一个合数，这样的$z$称为**Fermat witness**。

<div align=center>
<img src="https://i.imgur.com/IvRm9Ed.png" width="80%">
</div>

可以证明任意合数都至少存在一个Fermat witness。

<div align=center>
<img src="https://i.imgur.com/W4A63e7.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/fTluKV6.png" width="80%">
<img src="https://i.imgur.com/YRTJGdb.png" width="80%">
</div>

如果我们忽略Carmichael数的存在可以得到质数的检验算法：

<div align=center>
<img src="https://i.imgur.com/Ag3NzB5.png" width="80%">
<img src="https://i.imgur.com/DXZTyD2.png" width="80%">
<img src="https://i.imgur.com/S8jbbyT.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/qS0ILFx.png" width="80%">
</div>

## Bloom Filters

## Reference

- [Cryptography](https://teapowered.dev/assets/ga-notes.pdf#page=60)
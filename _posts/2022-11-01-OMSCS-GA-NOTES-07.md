---
layout: article
title: OMSCS-GA课程笔记07-Linear Programming
tags: ["CS6515-GA", "OMSCS"]
key: OMSCS-GA-07
aside:
  toc: true
sidebar:
  nav: OMSCS-GA
---

> 这个系列是Gatech OMSCS 高级算法课程([CS 6515: Intro to Grad Algorithms](https://omscs.gatech.edu/cs-6515-intro-graduate-algorithms))的同步课程笔记。课程内容涉及动态规划、随机算法、分治、图算法、最大流、线性规划以及NP完备等高级算法的设计思想和相关应用，本节主要介绍线性规划。
<!--more-->

## Linear Programming

**线性规划(linear programming, LP)**是求解优化问题的一种重要技术，很多问题都可以通过转换为优化问题的方式来使用LP进行求解。

<div align=center>
<img src="https://i.imgur.com/NYeay6m.png" width="80%">
</div>

### Examples

#### Max-Flow via LP

前面介绍过的[最大流](/2022/10/05/OMSCS-GA-NOTES-04.html)问题可以等价地表示为一个优化问题：我们为每条边上的流量设置一个变量$f_e$，这样优化目标即为所有变量之和$\sum_{e \in E} f_e$，而对应的约束包括$f_e$非负且小于等于容量$c_e$以及除源点和终点外所有节点的流入量等于流出量等。

<div align=center>
<img src="https://i.imgur.com/qZ37Vmv.png" width="80%">
</div>

#### Simple Production

LP的另一个常见例子是确定产品的最优配置。假设有两种产品A和B，A产品的利润是1而B产品的利润是6。客户对两种产品的最大需求分别为300和200，而生产两种产品分别需要1小时和3小时，总共可用的生产时间为700小时。我们的目标是确定两种产品的产量来最大化利润。

<div align=center>
<img src="https://i.imgur.com/XJ4b5bo.png" width="80%">
</div>

#### 2D LP

上述问题可以形式化为如下的最优化问题。

<div align=center>
<img src="https://i.imgur.com/GRpp0Ln.png" width="80%">
<img src="https://i.imgur.com/V11TRO6.png" width="80%">
</div>

实际上对于二维的LP问题还有非常直观的几何解释，其中所有变量能够取值的范围称为**可行域(feasible region)**。

<div align=center>
<img src="https://i.imgur.com/TJ4QHxb.png" width="80%">
</div>

由于目标函数是一个线性函数，待求优化问题等价于在可行域上选取一点使得目标函数对应直线方程有最大的截距。

<div align=center>
<img src="https://i.imgur.com/lO3y9xR.png" width="80%">
</div>

从上面的例子不难发现LP问题有如下特点：

- 最优解可能不是整数
- LP可以在多项式时间内求解
- 可行域一定是凸集
- 最优解一定在可行域的顶点上

<div align=center>
<img src="https://i.imgur.com/eC6BLBw.png" width="80%">
</div>

#### 3D Example

对于三维的情况同样可以形式化LP问题。

<div align=center>
<img src="https://i.imgur.com/vNRpmJu.png" width="80%">
<img src="https://i.imgur.com/QZb4NkF.png" width="80%">
</div>

三维LP问题也有直观的几何解释，它相当于在三维凸几何体上寻找目标函数的最优点。

<div align=center>
<img src="https://i.imgur.com/lZ43H1x.png" width="80%">
</div>

### Standard Form

对于更一般的情况，LP问题可以形式化为最优化包含n个变量的线性函数同时满足相应的线性约束。

<div align=center>
<img src="https://i.imgur.com/kmyoFp9.png" width="80%">
</div>

如果从线性代数的角度来认识，还可以得到更加紧凑的表达形式。

<div align=center>
<img src="https://i.imgur.com/BqPuHbf.png" width="80%">
</div>

显然这两种表达方式是相互等价的。

<div align=center>
<img src="https://i.imgur.com/4BbbebU.png" width="80%">
</div>

对于n维的情况我们很难直观地表示n维空间，不过此时的几何意义与低维情况是一样的。

<div align=center>
<img src="https://i.imgur.com/B8pUplW.png" width="80%">
</div>

由于LP问题的最优点一定是在凸集的边界点上，因此求解LP可以转换为计算凸集的边界点然后寻找目标函数的最大值。

<div align=center>
<img src="https://i.imgur.com/FvWXIrG.png" width="80%">
</div>

求解LP问题的常用算法如下：

<div align=center>
<img src="https://i.imgur.com/hkZ5QqI.png" width="80%">
</div>

### Simplex Algorithm

simplex算法会从零点开始不断寻找局部上能够增大目标函数的边界点。由于目标函数是凸的，当所有边界点上的函数值都小于当前点时说明已经找到了最优解。

<div align=center>
<img src="https://i.imgur.com/5BOD5wG.png" width="80%">
<img src="https://i.imgur.com/PljdQFe.png" width="80%">
</div>

## Geometry

从几何角度来看，LP问题中每个约束都相当于在n维空间中定义了一个**半空间(half space)**，而这些半空间的交集构成了问题的可行域。

<div align=center>
<img src="https://i.imgur.com/eFLiNBM.png" width="80%">
</div>

由于目标函数是凸函数，LP问题仅在可行域为空以及可行域或是目标函数无界这两种情况下没有解。

<div align=center>
<img src="https://i.imgur.com/86oyCCU.png" width="80%">
<img src="https://i.imgur.com/4wPYA0f.png" width="80%">
</div>

因此在求解LP问题之前首先要判断是否存在上述两种无解的情况。对于可行域是否为空的问题，我们只需要考虑LP的约束即可。此时需要引入一个新的变量z来构造不等式约束：

$$
A \mathbf{x} + z \leq b
$$

$$
\mathbf{x} \geq 0
$$

接着，我们通过最大化z来判断可行域是否为空。如果z是非负的则说明存在可行域，而如果z为负数则可行域为空。

<div align=center>
<img src="https://i.imgur.com/xSshKtw.png" width="80%">
</div>

对于如何检查是否无界的情况我们留到对偶性中进行讲解。

## Duality

LP问题的一大特点在于它的**对偶性(duality)**。当已知一个LP问题可以使用相应的算法进行求解来得到最优函数值，而如果已知函数值的可能取值能否验证是否存在相应的解呢？

<div align=center>
<img src="https://i.imgur.com/gIVpRzB.png" width="80%">
</div>

### Upper Bound

假设这个给定的函数值存在于可行域中，我们可以为线性约束赋予相应的系数来组合出目标函数。此时组合后不等式约束的右侧即为目标函数的上界。

<div align=center>
<img src="https://i.imgur.com/md9xmoO.png" width="80%">
</div>

### Dual LP

那么如何计算组合系数呢？我们可以假设每一个不等式约束的系数为$y_i$，然后它们加起来得到待定系数的不等式。对于不等式左边每一个未知数，我们要求它的系数至少为目标函数对应的系数。同时最小化不等式右端，这样就得到了一个新的最优化问题。不难发现这个新的优化问题与原问题有对偶的系数和形式，因此称为对偶问题。

<div align=center>
<img src="https://i.imgur.com/LXKDaXp.png" width="80%">
<img src="https://i.imgur.com/CSzIMCp.png" width="80%">
</div>

### General Form

更一般情况下的对偶形式可以表示如下：

<div align=center>
<img src="https://i.imgur.com/7yXQwhI.png" width="80%">
</div>

更进一步，对偶问题也可以转换为一个等价的LP问题，而它的对偶等价于原始LP问题：

<div align=center>
<img src="https://i.imgur.com/kBWUyxe.png" width="80%">
</div>

### Weak Duality

LP的**弱对偶(weak duality)**定理指出对偶问题的目标函数是原始问题的一个上界。

<div align=center>
<img src="https://i.imgur.com/TMLik46.png" width="80%">
</div>

更进一步，假设x和y分别是原始问题和对偶问题可行域中的点，如果两个优化问题的目标函数在该处有相同的值则说明x和y分别是两个问题的最优解。

<div align=center>
<img src="https://i.imgur.com/F2vZ6ZP.png" width="80%">
</div>

### Unbounded LP

弱对偶的另一个推论是如果原始LP是无界的则其对偶问题可行域为空；反之如果对偶问题是无界的则原始问题可行域为空。

<div align=center>
<img src="https://i.imgur.com/z2mz9kL.png" width="80%">
</div>

利用这个推论就可以验证原始LP是否有界，我们只需要考虑其对偶问题的可行域即可。这样判断LP是否有解就只需要判断原始问题和其对偶问题可行域是否为空。

<div align=center>
<img src="https://i.imgur.com/0Axh38B.png" width="80%">
</div>

### Strong Duality

LP的**强对偶(strong duality)**定理指出原始问题和对偶问题有解以及有最优解是相互等价的。

<div align=center>
<img src="https://i.imgur.com/IqfmIfU.png" width="80%">
</div>

## Max-SAT Approximation


## Reference

- [Linear Programming](https://teapowered.dev/assets/ga-notes.pdf#page=69)
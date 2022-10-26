---
layout: article
title: OMSCS-GA课程笔记06-NP Completeness
tags: ["CS6515-GA", "OMSCS"]
key: OMSCS-GA-06
aside:
  toc: true
sidebar:
  nav: OMSCS-GA
---

> 这个系列是Gatech OMSCS 高级算法课程([CS 6515: Intro to Grad Algorithms](https://omscs.gatech.edu/cs-6515-intro-graduate-algorithms))的同步课程笔记。课程内容涉及动态规划、随机算法、分治、图算法、最大流、线性规划以及NP完备等高级算法的设计思想和相关应用，本节主要介绍NP完备理论。
<!--more-->

## Computational Complexity

在本节课中我们会介绍**NP完备(NP-completeness)**的概念、P=NP以及P≠NP的意义、以及如何证明一个问题是**难以求解(intractable)**的。

<div align=center>
<img src="https://i.imgur.com/GP0NR3H.png" width="80%">
</div>

### Complexity Classes

我们定义NP问题是所有**搜索(search)**问题的集合，这里搜索是指可以在多项式时间内对它的解进行验证的问题。而P问题则是指可以在多项式时间内进行求解的搜索问题集合。显然P问题是NP问题的一个子集，这是因为能在多项式时间内求解的问题必然能在多项式时间内进行验证。

<div align=center>
<img src="https://i.imgur.com/DUw1b0Q.png" width="80%">
</div>

因此P=NP是指验证一个问题和求解这个问题具有相同的难度，而P≠NP则是指验证一个问题要比求解这个问题要困难一些。

<div align=center>
<img src="https://i.imgur.com/yWyTnxY.png" width="80%">
</div>

### Search Problem

对于搜索问题，我们可以形式化地定义如下：

<div align=center>
<img src="https://i.imgur.com/I0M3Iv8.png" width="80%">
</div>

#### SAT

我们在前面课程中介绍的[SAT问题](/2022/10/04/OMSCS-GA-NOTES-03.html#sat-problem)就是一个NP问题。

<div align=center>
<img src="https://i.imgur.com/ciU96OZ.png" width="80%">
<img src="https://i.imgur.com/PIfCD67.png" width="80%">
</div>

#### GCP

**图着色问题(graph coloring problem, GCP)**是图论中的经典问题，对于给定的k种颜色我们希望可以保证着色后相邻节点有着不同的颜色。显然GCP同样也是NP问题。

<div align=center>
<img src="https://i.imgur.com/xG7fwDS.png" width="80%">
</div>

#### MST

[最小生成树](/2022/10/04/OMSCS-GA-NOTES-03.html#minimum-spanning-tree)同样是NP问题，实际上它还是P问题。

<div align=center>
<img src="https://i.imgur.com/lp1UxVR.png" width="80%">
<img src="https://i.imgur.com/Q6CKnrb.png" width="80%">
</div>

#### Knapsack

而[knapsack问题](/2022/08/23/OMSCS-GA-NOTES-01.html#knapsack)可以利用动态规划进行求解，但目前人们无法证明knapsack问题是否是一个NP问题，也无法证明它是否是一个P问题。

<div align=center>
<img src="https://i.imgur.com/AN8ou24.png" width="80%">
<img src="https://i.imgur.com/GGQz3Mi.png" width="80%">
<img src="https://i.imgur.com/SyhJz94.png" width="80%">
<img src="https://i.imgur.com/be0Hlv5.png" width="80%">
</div>

不过knapsack问题存在一个变体，我们引入一个新的变量g同时要求背包内物品的价值之和至少为g。此时的knapsack问题则是一个NP问题。

<div align=center>
<img src="https://i.imgur.com/tk0usPq.png" width="80%">
<img src="https://i.imgur.com/qClPNE1.png" width="80%">
</div>

### NP-Completeness

总结一下，在计算复杂度理论中P是指多项式时间(polynomial time)，而NP则是指nondeterministic polynomial time。

<div align=center>
<img src="https://i.imgur.com/ekjOJc8.png" width="80%">
</div>

由于P是NP的子集，我们关心的是是否每个NP问题同样是P问题，即P是否等于NP。

<div align=center>
<img src="https://i.imgur.com/W7gCrui.png" width="80%">
</div>

如果P≠NP那么在NP问题中一定存在一些难以求解的问题，称为**NP完备(NP-completeness)**问题。用Venn图来表示的话NP完备问题是NP问题和P问题的差集。NP完备问题是NP问题中最困难的问题，显然如果P≠NP那么NP完备问题一定不是P问题。它的逆否命题则说明如果能够找到一个NP完备问题在多项式时间内的解，那么所有NP问题都是P问题，即P=NP。

<div align=center>
<img src="https://i.imgur.com/esCVci4.png" width="80%">
</div>

如果我们承认P≠NP，那么上面提到的SAT问题就是一个典型的NP完备问题。

<div align=center>
<img src="https://i.imgur.com/ZF34chs.png" width="80%">
</div>

### Reductions

要证明一个问题是NP完备需要使用**归约(reduction)**的技巧。具体来说对于两个问题A和B，我们需要证明求解问题A可以转换为求解问题B，或者求解问题A最多相当于求解问题B，即求解B问题一定可以求解出A问题。如果我们可以在多项式时间内解决B问题，那么一定可以在多项式时间内解决A问题。

<div align=center>
<img src="https://i.imgur.com/iYR0qxW.png" width="80%">
</div>

假设问题A为图着色问题，问题B为SAT问题。利用归约可以证明图着色问题为NP完备问题。

<div align=center>
<img src="https://i.imgur.com/sD6Xuta.png" width="80%">
<img src="https://i.imgur.com/ul4S1vS.png" width="80%">
</div>

总结一下证明某个问题是NP完备问题需要两步：

- 证明该问题是NP问题
- 证明所有NP问题可以归约到该问题

由于我们已知SAT问题是NP完备问题，因此对于第二步可以通过归约将SAT归约到所需问题上来进行证明。

<div align=center>
<img src="https://i.imgur.com/wdFDqAt.png" width="80%">
<img src="https://i.imgur.com/DUovPSe.png" width="80%">
<img src="https://i.imgur.com/4uDUir0.png" width="80%">
</div>

## 3SAT

这一节我们开始证明3SAT问题是NP完备问题。

<div align=center>
<img src="https://i.imgur.com/yRgz4FU.png" width="80%">
<img src="https://i.imgur.com/4mh461I.png" width="80%">
<img src="https://i.imgur.com/B3kZ8oa.png" width="80%">
</div>

首先我们需要证明3SAT是NP问题。显然验证3SAT的解只需要$O(m)$的时间复杂度，因此3SAT是NP问题。

<div align=center>
<img src="https://i.imgur.com/Am3iGQn.png" width="80%">
</div>

接下来证明SAT可以归约到3SAT上，具体来说我们需要证明任意SAT问题可以转换为求解一个3SAT问题。

<div align=center>
<img src="https://i.imgur.com/waCrPMC.png" width="80%">
<img src="https://i.imgur.com/JA1bOeJ.png" width="80%">
</div>

假设有一个包含4个变量的从句$C$：

$$
C = ( \bar{x}_2 \vee x_3 \vee \bar{x}_1 \vee \bar{x}_4 )
$$

我们定义一个新的从句$C'$，它由2个只包含3个变量的从句构成：

$$
C' = ( \bar{x}_2 \vee x_3 \vee y ) \wedge ( \bar{y} \vee \bar{x}_1 \vee \bar{x}_4 )
$$

可以证明$C$和$C'$是等价的，这样一个4SAT问题就转换成了3SAT。

<div align=center>
<img src="https://i.imgur.com/1ztyGfr.png" width="80%">
<img src="https://i.imgur.com/lGxX2C8.png" width="80%">
</div>

实际上对于包含k个变量的从句$C$我们都可以把它转换为只包含3个变量的从句$C'$：

<div align=center>
<img src="https://i.imgur.com/IUVHmN5.png" width="80%">
<img src="https://i.imgur.com/HdJHynK.png" width="80%">
<img src="https://i.imgur.com/Iam7DFu.png" width="80%">
</div>

这样就可以把SAT问题归约到3SAT上，即3SAT是NP完备问题。

<div align=center>
<img src="https://i.imgur.com/H6Eq1ne.png" width="80%">
<img src="https://i.imgur.com/uLkrjbb.png" width="80%">
<img src="https://i.imgur.com/dHSydop.png" width="80%">
</div>

## Graph Problems

## Knapsack

## Halting Problem

## Reference

- [Computational Complexity](https://teapowered.dev/assets/ga-notes.pdf#page=82)
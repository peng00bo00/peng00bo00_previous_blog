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

而[knapsack问题](/2022/08/23/OMSCS-GA-NOTES-01.html#knapsack)可以利用动态规划进行求解，但实际上人们无法证明knapsack问题是否是一个NP问题，也无法证明它是否是一个P问题。

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

如果P≠NP那么在NP问题中一定存在一些难以求解的问题，称为**NP完备(NP-completeness)**问题。用Venn图来表示的话NP完备问题是NP问题和P问题的差集。NP完备问题是NP问题中最困难的问题，显然如果P≠NP那么NP完备问题一定不是P问题。它的逆否命题则说明如果能够找到一个NP完备问题在多项式时间内的解，那么所有NP完备问题都是P问题。

<div align=center>
<img src="https://i.imgur.com/esCVci4.png" width="80%">
</div>

上面提到的SAT问题就是一个典型的NP完备问题。

<div align=center>
<img src="https://i.imgur.com/ZF34chs.png" width="80%">
</div>

### Reductions

要证明一个问题是NP完备需要使用**归约(reduction)**的技巧。具体来说对于两个问题A和B，我们需要证明求解问题A可以转换为求解问题B，或者求解问题A最多相当于求解问题B，即求解B问题一定可以求解出A问题。如果我们可以在多项式时间内解决B问题，那么一定可以在多项式时间内解决A问题。

<div align=center>
<img src="https://i.imgur.com/iYR0qxW.png" width="80%">
</div>

## 3SAT

## Graph Problems

## Knapsack

## Halting Problem

## Reference

- [Computational Complexity](https://teapowered.dev/assets/ga-notes.pdf#page=82)
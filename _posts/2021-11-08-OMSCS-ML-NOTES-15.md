---
layout: article
title: OMSCS-ML课程笔记15-Game Theory
tags: ["OMSCS", "CS7641-ML"]
key: OMSCS-ML-15
aside:
  toc: true
sidebar:
  nav: OMSCS-ML
---

> 这个系列是Gatech OMSCS 机器学习课程([CS 7641: Machine Learning](https://omscs.gatech.edu/cs-7641-machine-learning))的同步课程笔记。课程内容涉及监督学习、无监督学习和强化学习三个部分，本节介绍博弈论的相关内容。
<!--more-->

## Games

**博弈论(game theory)**是研究个体之间如何相互合作竞争并寻找最优策略的学科。和强化学习相比，博弈论的特点是同一个系统中有多个**玩家(player)**，同时每个玩家都想要在博弈过程中最大化自身的收益。博弈论在现实生活中的应用已经超出了计算机科学的范畴，在金融市场、军事战略甚至社会科学中都能见到博弈论的身影。

### Minimax

最简单的博弈只包含2个玩家，且他们之间的信息是对等的。我们称这样的博弈为**2-player, zero-sum, finite, deterministic game with perfect information**：

- 2-player是指只有2个玩家；
- zero-sum是指博弈是零和的，两个玩家的收益之和为0；
- finite是指玩家的状态和策略都是有限的；
- deterministic是指系统是确定的，没有随机因素；
- perfect information是指两个玩家都能获得全部的信息。

我们通过一个简单的例子来进行介绍。假设博弈过程可以通过如下图所示的树来表示，其中节点表示状态边表示玩家可选的行为。由$A$玩家先行从状态1中选择向左或是向右，然后$B$选择下一个动作，再回到$A$进行选择。当状态到达叶节点时游戏结束，叶节点对应的数字为玩家$A$的收益(由于是零和博弈，玩家$B$的收益为它的相反数)。玩家$A$的目标是最大化收益，相应地玩家$B$的目标是最小化收益。

<div align=center>
<img src="https://i.imgur.com/zCx3SnZ.png" width="30%">
</div>

根据玩家$A$和玩家$B$所有可能的行为，我们可以利用一个矩阵来表示整个博弈过程的所有可能结果，如下图所示：

<div align=center>
<img src="https://i.imgur.com/LdhuXXd.png" width="30%">
</div>

矩阵的每一行表示玩家$A$采取的行为(策略)，每一列表示玩家$B$采取的行为(策略)；矩阵中的每个元素表示玩家$A$和玩家$B$的行为所导致的最终收益。对于玩家$A$来说，无论他做出什么样的选择玩家$B$都会试图最小化收益，因此$A$的最优策略是选择第2行；类似地，对玩家$B$而言，玩家$A$会试图最大化每一列的数字，因此玩家$B$的最优策略是选择第2列。

上文所述的过程实际上就是minimax算法。我们假设自身是玩家$A$，我们需要在玩家$B$最小化收益的策略中选择收益最大的那个策略，该策略即为最优策略。实际上Von Neumann证明了对于2-player, zero-sum, finite, deterministic game with perfect information，每个玩家都存在最优策略，即minimax=maximin。

### Relaxation: Non-Determinism

### Relaxation: Hidden Information

### Prisoner’s Dilemma

### Nash Equilibrium

## Reference

- [Wikipedia: Minimax](https://en.wikipedia.org/wiki/Minimax)
- [Wikipedia: Minimax theorem](https://en.wikipedia.org/wiki/Minimax_theorem)
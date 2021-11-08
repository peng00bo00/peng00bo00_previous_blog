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
<img src="https://i.imgur.com/zCx3SnZ.png" width="40%">
</div>

根据玩家$A$和玩家$B$所有可能的行为，我们可以利用一个矩阵来表示整个博弈过程的所有可能结果，如下图所示：

<div align=center>
<img src="https://i.imgur.com/LdhuXXd.png" width="30%">
</div>

矩阵的每一行表示玩家$A$采取的行为(策略)，每一列表示玩家$B$采取的行为(策略)；矩阵中的每个元素表示玩家$A$和玩家$B$的行为所导致的最终收益。对于玩家$A$来说，无论他做出什么样的选择玩家$B$都会试图最小化收益，因此$A$的最优策略是选择第2行；类似地，对玩家$B$而言，玩家$A$会试图最大化每一列的数字，因此玩家$B$的最优策略是选择第2列。

上文所述的过程实际上就是minimax算法。我们假设自身是玩家$A$，我们需要在玩家$B$最小化收益的策略中选择收益最大的那个策略，该策略即为最优策略。实际上Von Neumann证明了对于2-player, zero-sum, finite, deterministic game with perfect information，每个玩家都存在最优策略且他们的按照最优策略行动的话博弈过程的解是确定的，即minimax=maximin。

### Relaxation: Non-Determinism

接下来我们放松一下系统的限制，假设系统存在随机性。以下图为例，当系统状态到达方块的位置时我们可能会依据概率得到不同的收益：

<div align=center>
<img src="https://i.imgur.com/grhs70u.png" width="40%">
</div>

在这种情况下我们只需要用收益的期望来代替原本的收益即可，这样就可以得到这个博弈过程的矩阵表示：

<div align=center>
<img src="https://i.imgur.com/AkP40b6.png" width="20%">
</div>

### Relaxation: Hidden Information

我们进一步放松对系统的限制，假设现在玩家不再具有全部的信息。这里我们还是用一个例子进行说明：假设玩家$A$在开局会得到红色或是黑色的牌且这张牌只有他自己可见。如果$A$开始获得的是红色的牌则$A$可以选择hold或是resign，如果是hold收益由$B$的行为来决定，而如果$A$选择resign则会获得-20的收益。类似地，如果$A$开始获得的是黑色的牌则他必须选择hold，最终的收益仍然由$B$的行为来决定。整个博弈过程可以利用下图所示的树来表示：

<div align=center>
<img src="https://i.imgur.com/ebYkGCF.png" width="40%">
</div>

我们同样利用收益的期望来计算不同策略的收益，从而得到收益矩阵如下所示：

<div align=center>
<img src="https://i.imgur.com/FfXI2eN.png" width="30%">
</div>

此时从$A$的角度上看他无论选择hold还是resign都会得到-5的收益，但从$B$的角度上看他会选择see从而得到5的收益。此时$A$和$B$按照最优策略行动会得到不同的解，这说明由于隐藏信息的存在会导致minimax $\neq$ maximin。

实际上如果玩家$B$知道$A$的行为模式的话仍然可以保证minimax=maximin。假设当$A$手上的是红牌的时候他会选择resign而且$B$也知道这点，那么当$A$选择了hold时$B$一定会选择resign从而最小化收益。

### Mixed Strategies

所谓的mixed strategy是指关于关于策略的分布。我们假设$A$会以$P$的概率选择hold这个行为，同时假设$B$永远会选择resign，则当前策略下$A$的收益为：

$$
\begin{aligned}
\mathbb{E}[\text{profit}] &= (0.5 \times 10) + (0.5 \times ((P \times 10) + ((1-P) \times (-20)))) \\
&= 15 P - 5
\end{aligned}
$$

类似地，如果$B$永远会选择see则$A$的收益为：

$$
\begin{aligned}
\mathbb{E}[\text{profit}] &= (0.5 \times 30) + (0.5 \times ((P \times -40) + ((1-P) \times -20))) \\
&= -10 P + 5
\end{aligned}
$$

接下来我们把这两种情况下$A$的收益函数画在一张图上，得到它们的交点$P=0.4$。这个点表示当$P$取0.4时，无论$B$采取什么样的策略(pure strategy或者mixed strategy)$A$获得的期望收益都是相同的。但需要注意的是这一点并不意味着最优概率或是最优收益。

<div align=center>
<img src="https://i.imgur.com/qsrX1jm.png" width="40%">
</div>

### Prisoner’s Dilemma

接下来我们再去掉零和博弈的约束，然后介绍著名的**囚徒困境(prisoner’s dilemma)**：

- 假设有两个囚犯分开接受审讯；
- 每个囚徒可以选择保持沉默或是向警方招供；
- 如果两名囚犯都保持沉默的话每个人获得1年的刑期；
- 如果两名囚犯都招供的话每个人获得6年的刑期；
- 如果一名囚犯招供而另一名囚犯保持沉默，则招供的可以免罪而保持沉默的获得9年刑期。

整个博弈过程的收益可以用如下所示的矩阵来表示：

<div align=center>
<img src="https://i.imgur.com/GaABC13.png" width="40%">
</div>

对于每一名囚犯来说他的最优策略都是选择招供，这是因为此时无论另一名囚犯如何选择他的刑期都是最短的。但在这种情况下两个人都会获得6年的刑期，而如果两个人都保持沉默的话每个人只有1年的刑期。换句话说每名囚犯的最优策略并不会导致总体的最优，要想达到总体最优每名囚犯的策略都依赖于另一名囚犯的策略。

### Nash Equilibrium

囚徒困境对于多名玩家的情况同样成立。假设有$n$名玩家，每名玩家可行的策略为集合$s_i$，我们称策略$s_1^* \in s_1, s_2^* \in s_2, ..., s_n^* \in s_n$达到了**Nash均衡(Nash equilibrium)**当且仅当对每名玩家有：

$$
s_i^* = \arg \max_{s_i} U(s_1^*, ..., s_i, ..., s_n^*)
$$

## Reference

- [Wikipedia: Minimax](https://en.wikipedia.org/wiki/Minimax)
- [Wikipedia: Minimax theorem](https://en.wikipedia.org/wiki/Minimax_theorem)
- [Wikipedia: Prisoner's dilemma](https://en.wikipedia.org/wiki/Prisoner%27s_dilemma)
- [Wikipedia: Nash equilibrium](https://en.wikipedia.org/wiki/Nash_equilibrium)
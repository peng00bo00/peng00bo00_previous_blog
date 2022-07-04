---
layout: article
title: OMSCS-RL课程笔记10-Generalizing Generalizing
tags: ["OMSCS", "CS7642-RL"]
key: OMSCS-RL-10
aside:
  toc: true
sidebar:
  nav: OMSCS-RL
---

> 这个系列是Gatech OMSCS 强化学习课程([CS 7642: Reinforcement Learning](https://omscs.gatech.edu/cs-7642-reinforcement-learning))的同步课程笔记。课程内容涉及强化学习算法的理论和相关应用，本节课介绍强化学习的一些难点和相关的处理方法。
<!--more-->

## What makes RL hard?

我们首先来考虑一下为什么强化学习比较困难的问题。和监督学习相比强化学习的奖励是滞后的，这意味着我们无法按照函数拟合的方式去学习一个好的策略；另一方面，在强化学习中智能体需要对环境进行探索才能从基类到的经验进行学习；除此之外，强化学习的规模往往是非常巨大的，价值函数的规模同时依赖于状态空间和行为空间的大小。

<div align=center>
<img src="https://i.imgur.com/Gugdu3h.png" width="80%">
</div>

## Temporal Abstraction

假设智能体位于方格世界中，它的目标是前往右下角的房间并获取奖励+1。这样的问题可以使用强化学习来求解，并得到对应的策略$\pi$。显然，当智能体进行决策时需要把每一时刻的状态输入到策略$\pi$中，这就导致了整个问题的规模无比巨大。而对于人来说，我们不需要考虑所有时刻的状态而是选取某些关键的状态来对问题进行抽象。在本例中，我们可以把策略重新定义为首先移动到右边的房间，然后再移动到下方的房间。这样整个问题就可以使用这些新定义的状态和行为来缩减求解的规模。这样的思想称为**temporal abstraction**。

<div align=center>
<img src="https://i.imgur.com/T31idlu.png" width="80%">
<img src="https://i.imgur.com/fVxvRMQ.png" width="80%">
</div>

实际上，我们甚至可以使用这些抽象出的状态来重新定义和求解强化学习的问题。

<div align=center>
<img src="https://i.imgur.com/1tZSkvQ.png" width="80%">
</div>

### Option Function

要使用temporal abstraction来求解强化学习问题我们首先需要引入**option**的概念：

<div align=center>
<img src="https://i.imgur.com/JdBFNxt.png" width="80%">
</div>

在option的基础上可以重新推导Bellman方程如下：

$$
V_{t+1}(s) = \max_{o} \bigg( R(s, o) + \sum_{s'} F(s, o, s') V_t(s') \bigg)
$$

不过需要注意的是上式中不包含折扣系数$\gamma$，实际上它位于奖励函数中：

$$
R = \mathbb{E} [r_1 + \gamma r_2 + \gamma^3 r_3 + \cdots + \gamma^{k-1} r_k]
$$

类似地，$F$则表示从状态$s$出发经过$k$步之后位于$s'$的折扣期望：

$$
F = \mathbb{E} [\gamma^k \Delta_{s_k, s'} \vert s, k \ \text{steps}]
$$

这样相当于在原始问题的基础上重新定义了一个新的MDP，称为**semi-MDP(SMDP)**。

<div align=center>
<img src="https://i.imgur.com/kpHTECS.png" width="80%">
</div>

更进一步可以证明求解SMDP同样可以获得它所定义的最优策略，尽管这个策略在大多数情况下不等于原始MDP的最优策略，但它仍然是一个足够好的解。同时求解SMDP的代价往往要远小于求解原始MDP，这对于求解大规模的MDP是有益的。

<div align=center>
<img src="https://i.imgur.com/w0iyj9U.png" width="80%">
</div>

## Goal Abstraction

除了temporal abstraction之外，我们还可以对总体目标进行分解然后通过求解每个小目标来实现最终的目标。从这样的角度来看总体目标可以看做是若干个相互平行的小目标。

<div align=center>
<img src="https://i.imgur.com/kh9MeOD.png" width="80%">
</div>

此时我们可以对不同的目标进行模块化，这样的强化学习问题称为**modular RL**。常用求解modular RL的算法包括greatest mass Q-learning, top Q-learning, negotiated Q-learning等。

<div align=center>
<img src="https://i.imgur.com/SVYK0Sa.png" width="80%">
</div>

## Monte-Carlo Tree Search
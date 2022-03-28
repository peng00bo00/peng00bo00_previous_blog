---
layout: article
title: OMSCS-DL课程笔记17-Deep Reinforcement Learning
tags: ["OMSCS", "CS7643-DL"]
key: OMSCS-DL-17
aside:
  toc: true
sidebar:
  nav: OMSCS-DL
---

> 这个系列是Gatech OMSCS 深度学习课程([CS 7643: Deep Learning](https://omscs.gatech.edu/cs-7643-deep-learning))的同步课程笔记。课程内容涉及深度学习的基本理论方法以及它在计算机视觉、自然语言处理以及决策理论等领域中的应用，本节主要介绍深度强化学习。
<!--more-->

## Reinforcement Learning Introduction

到目前为止本课程主要介绍了深度学习在**监督学习(supervised learning)**中的应用，除了监督学习之外机器学习的范畴还包括**无监督学习(unsupervised learning)**以及**强化学习(reinforcement learning)**。

<div align=center>
<img src="https://i.imgur.com/Gznqv8G.png" width="80%">
</div>

强化学习的目标是求解一个序列决策问题。我们希望**智能体(agent)**能够通过与**环境(environment)**的互动和反馈来学习到合适的**策略(policy)**，从而最大化**奖励(reward)**。

<div align=center>
<img src="https://i.imgur.com/MLccZod.png" width="80%">
</div>

和监督学习相比，强化学习不存在一个明确的学习目标，智能体只能通过环境给出的反馈信号进行学习。同时反馈信号往往是滞后的，即在很多情况下只会在最后一步才能得到奖励。

<div align=center>
<img src="https://i.imgur.com/pjGwPp8.png" width="80%">
</div>

强化学习的常见难点如下：

<div align=center>
<img src="https://i.imgur.com/wZqRRE5.png" width="80%">
</div>

从更严格的角度来看，强化学习可以按照如下方式进行建模。在任意时刻$t$，智能体根据观测$o_t$执行了行为$a_t$，而环境则根据智能体给出的行为返回下一时刻的观测$o_{t+1}$以及奖励$r_{t+1}$。

<div align=center>
<img src="https://i.imgur.com/5RGITe3.png" width="80%">
</div>

目前强化学习在很多领域都取得了令人瞩目的研究成果。

<div align=center>
<img src="https://i.imgur.com/OieyUok.png" width="80%">
<img src="https://i.imgur.com/Eu0dWno.png" width="80%">
<img src="https://i.imgur.com/yRuLp0m.png" width="80%">
</div>

## Markov Decision Processes

### MDPs in the Context of RL

要严格介绍强化学习则需要引入**Markov决策过程(Markov decision process, MDP)**。一个MDP包括状态空间$\mathcal{S}$、行为空间$\mathcal{A}$、奖励函数$\mathcal{R}(s, a, s')$、转移概率$\mathbb{T}(s, a, s')$以及折扣系数$\gamma$。同时MDP假定了转移概率$\mathbb{T}(s, a, s')$满足一阶Markov性，即$t$时刻到$t+1$时刻的转移概率只与$t$时刻的状态和行为有关，与状态和行为的历史无关。

<div align=center>
<img src="https://i.imgur.com/unY51D3.png" width="80%">
</div>

在强化学习中转移概率和奖励函数对于智能体是未知的，智能体只能通过和环境的互动来学习最优策略。当然在编程时程序员是需要知道转移概率和奖励函数的，毕竟这样才能编写出运行环境。

<div align=center>
<img src="https://i.imgur.com/n9x5dKO.png" width="80%">
</div>

以二维格子世界为例，智能体从三角形位置出发到达对应的格子时会获得相应的奖励。这个MDP的状态空间包括所有格子的坐标，行为空间为上下左右四个可能的前进方向，而奖励函数则是在指定格子上得到的反馈。需要说明的是环境的转移概率往往不是确定的，因此智能体实际的行为不一定完全符合规划的预期。

<div align=center>
<img src="https://i.imgur.com/J8huydN.png" width="80%">
</div>

### Solving MDPs: Optimal Policy

求解MDP意味着寻找到当前环境下的**最优策略(optimal policy)**。智能体的策略可以是确定性的也可以是随机的，而一个好的策略不仅仅要考虑当前状态下的奖励，更要保证在将来的状态中有着比较高的奖励。

<div align=center>
<img src="https://i.imgur.com/Wzd8isN.png" width="80%">
</div>

我们为每一时刻$t$获得的奖励乘上一个折扣系数$\gamma^t$，定义策略$\pi$的回报为按照该策略执行后未来所有可能状态奖励的期望。这样最优策略$$\pi^*$$就是最大化这个折扣后奖励期望的策略。

<div align=center>
<img src="https://i.imgur.com/w8rXGON.png" width="80%">
</div>

### Discounting Future Rewards

之所以考虑折扣后的奖励一方面是为了保证奖励序列可以收敛，另一方面通过折扣系数来控制智能体更关注于近期的奖励。一般来说$\gamma$越趋向于1越关注长期的奖励，而$\gamma$越趋向于0则会更关注短期的奖励。

<div align=center>
<img src="https://i.imgur.com/k05gjTz.png" width="80%">
</div>

### Value Function

描述未来折扣后奖励期望的函数称为**价值函数(value function)**。在强化学习中包括两种价值函数：首先是描述状态$s$自身好坏的函数，称为**状态价值函数(state value function)**记为$V(s)$；另一种是描述在状态$s$下采取行为$a$的好坏的价值函数，称为**状态-行为价值函数(state-action value function)**记为$Q(s, a)$。

<div align=center>
<img src="https://i.imgur.com/YbIJ9Qe.png" width="80%">
</div>

状态价值函数定义为从$s$状态出发按照策略$\pi$选择动作后所有可能轨迹的折扣回报之和的期望。

<div align=center>
<img src="https://i.imgur.com/FMQnnsG.png" width="80%">
</div>

状态-行为价值函数与之类似，只不过除了$s$状态还需要考虑该时刻的行为$t$作为条件再计算期望。

<div align=center>
<img src="https://i.imgur.com/T5cAfEc.png" width="80%">
</div>

## Algorithms for Solving MDPs

## Deep Q-Learning

## Policy Gradients, Actor-Critic
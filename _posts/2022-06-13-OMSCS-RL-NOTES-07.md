---
layout: article
title: OMSCS-RL课程笔记07-Exploring Exploration
tags: ["OMSCS", "CS7642-RL"]
key: OMSCS-RL-07
aside:
  toc: true
sidebar:
  nav: OMSCS-RL
---

> 这个系列是Gatech OMSCS 强化学习课程([CS 7642: Reinforcement Learning](https://omscs.gatech.edu/cs-7642-reinforcement-learning))的同步课程笔记。课程内容涉及强化学习算法的理论和相关应用，本节主要介绍强化学习中的探索问题。
<!--more-->

**探索(explore)**是强化学习中非常重要的概念，甚至可以说"探索"是强化学习与通常意义下机器学习的主要区别。在本节课中我们会从赌博机模型、确定性MDP以及随机MDP三个方面来讨论探索在强化学习中的意义。

## Bandits

### K-armed Bandits

**K臂赌博机模型(K-armed bandits)**是经典的强化学习问题。在K臂赌博机模型中一共有K个不同的赌博机，每一轮游戏中智能体需要选择其中的一个，然后选择的机器会根据自身设置的概率给予智能体0或1作为奖励。智能体的目标是最大化累计奖励，也即选择回报概率最大的机器。由于智能体对每个机器的奖励概率一无所知，因此它需要首先对每个机器进行探索从而对概率进行建模。

<div align=center>
<img src="https://i.imgur.com/t4xpV8F.png" width="80%">
</div>

### Confidence-Based Exploration

当智能体对每个赌博机进行一定的探索后就可以利用这些经验来选择最优的机器。最直观的方法是利用这些数据来计算每个机器给出奖励的概率，其中概率最大的机器即为智能体的最优选择。显然当观测到的样本数不足时对概率的估计会具有很大的误差，此时智能体的选择往往是错误的。从这个角度上讲智能体在每一次进行决策时需要考虑是否利用当前观测到的数据执行最优策略还是继续对环境进行探索，这样的问题称为**exploration-exploitation困境(exploration-exploitation dilemma)**。

<div align=center>
<img src="https://i.imgur.com/Nzs8yKo.png" width="80%">
</div>

### Metrics for Bandits

我们需要建立某种指标来平衡智能体的exploration和exploitation行为。这样当智能体基于该指标进行决策时可以找到最优的机器并获得最大累计奖励。有时可能没有办法在有限的探索中计算出最优的机器，但我们希望基于该指标仍然可以在多项式时间内以一个比较大的概率寻找到近似最优的机器。

<div align=center>
<img src="https://i.imgur.com/FOICW0a.png" width="80%">
<img src="https://i.imgur.com/z6CCINn.png" width="80%">
<img src="https://i.imgur.com/HZCqNSU.png" width="80%">
<img src="https://i.imgur.com/PIU57yB.png" width="80%">
<img src="https://i.imgur.com/Hxc0XSM.png" width="80%">
<img src="https://i.imgur.com/PhGiUn6.png" width="80%">
</div>

### Hoeffding Bound

实际上对于K臂赌博机问题我们可以利用**Hoeffding界(Hoeffding bound)**作为概率估计的置信区间。

<div align=center>
<img src="https://i.imgur.com/m2i9u7n.png" width="80%">
</div>

更进一步还可以利用Hoeffding bound来选择最优的机器。

<div align=center>
<img src="https://i.imgur.com/RffAMQ9.png" width="80%">
<img src="https://i.imgur.com/il37pKo.png" width="80%">
</div>

除此之外，也可以利用Hoeffding bound来计算获得可靠估计所需的样本数。

<div align=center>
<img src="https://i.imgur.com/dTgXWdn.png" width="80%">
</div>

## Exploring Deterministic MDPs

## General Stochastic MDPs
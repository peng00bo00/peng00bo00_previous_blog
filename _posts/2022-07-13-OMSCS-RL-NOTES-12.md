---
layout: article
title: OMSCS-RL课程笔记12-Game Theory Reloaded
tags: ["OMSCS", "CS7642-RL"]
key: OMSCS-RL-12
aside:
  toc: true
sidebar:
  nav: OMSCS-RL
---

> 这个系列是Gatech OMSCS 强化学习课程([CS 7642: Reinforcement Learning](https://omscs.gatech.edu/cs-7642-reinforcement-learning))的同步课程笔记。课程内容涉及强化学习算法的理论和相关应用，本节课继续介绍博弈论的相关知识。
<!--more-->

## Iterated Prisoner's Dilemma

我们考虑需要进行**无限次重复博弈的囚徒困境问题(iterated Prisoner's Dilemma, IPD)**。在不断的博弈过程中由于Nash均衡的存在，两名囚徒实际上永远不会去选择改变自身的行为。

<div align=center>
<img src="https://i.imgur.com/IA5fIZU.png" width="80%">
</div>

然后我们引入折扣系数$\gamma$，它表示在每一轮的博弈后以$\gamma$的概率继续进行下一次博弈。利用几何级数，我们可以计算出博弈次数的期望为$\frac{1}{1-\gamma}$。

<div align=center>
<img src="https://i.imgur.com/BY54yLB.png" width="80%">
</div>

## Tit for Tat

对于这种依概率终止的博弈问题，一种经典的策略是**以牙还牙(tit for tat)**：此时的囚犯会选择在首次博弈中进行合作，然后接下来每一轮则采用与对手上一轮相同的行为。在这种情况下囚犯的策略可以描述为如下所示的状态机模型：

<div align=center>
<img src="https://i.imgur.com/3cgDZjN.png" width="80%">
</div>

另一名囚犯作为回应，在不同的策略下会得到不同的反馈，而且反馈值取决于系数$\gamma$。当$\gamma$值比较小时的最优策略是选择招供，而当$\gamma$值比较大时则会倾向于进行合作。

<div align=center>
<img src="https://i.imgur.com/Kh2g34U.png" width="80%">
</div>

## Finite State Strategy

利用状态机模型我们实际上可以把策略表示为一张图，图中黑色的部分是囚徒自己的行为，而绿色的部分则是对方的行为，而图中的数字则是双方在给定行为下囚徒得到的收益。不难发现此时囚犯的行为类似于一个MDP，只不过状态转移取决于对方的行为。

<div align=center>
<img src="https://i.imgur.com/EglcOyu.png" width="80%">
</div>

## Best Response in IPD

在IPD问题中囚犯的最优策略取决于对方的策略。比如说当对方选择一直合作时我们的最优策略是选择招供，而当对方选择招供时我们的最优策略同样是选择招供，此时两名囚犯都达到了Nash均衡。比较有趣的一点在于当双方都选择以牙还牙的策略时系统同样达到了Nash均衡，而且此时两名囚犯还会获得最大的总体收益，这表示在囚徒困境中仍然存在进行合作的可能。

<div align=center>
<img src="https://i.imgur.com/bHRFh0K.png" width="80%">
</div>

## Folk Theorem

实际上folk theorem指出在重复博弈中，**对等报复(retaliation)**的存在会使得博弈双方产生合作。

<div align=center>
<img src="https://i.imgur.com/hp6l6hx.png" width="80%">
<img src="https://i.imgur.com/deH8CUs.png" width="80%">
</div>

## Repeated Games


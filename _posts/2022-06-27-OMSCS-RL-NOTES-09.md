---
layout: article
title: OMSCS-RL课程笔记09-Partially Observable MDPs
tags: ["OMSCS", "CS7642-RL"]
key: OMSCS-RL-09
aside:
  toc: true
sidebar:
  nav: OMSCS-RL
---

> 这个系列是Gatech OMSCS 强化学习课程([CS 7642: Reinforcement Learning](https://omscs.gatech.edu/cs-7642-reinforcement-learning))的同步课程笔记。课程内容涉及强化学习算法的理论和相关应用，本节主要介绍部分可观察MDP。
<!--more-->

## POMDPs

**部分可观察MDP(partially observable MDP, POMDP)**是对标准MDP的推广，基于POMDP的框架我们可以去讨论一些非马尔科夫的环境下智能体的决策问题。在POMDP中环境仍然是一个标准的MDP，但智能体无法直接获得系统的状态而是通过一个观测函数$O$来获得对状态$s$的观测$z$。在很多情况下系统状态$s$和观测$z$之间的关系是不确定的，它们的概率可记为$P(z \vert s) = O(s, z)$。

<div align=center>
<img src="https://i.imgur.com/Vv6zMTx.png" width="80%">
</div>

## State Estimation

显然在POMDP中智能体的核心问题在于如何估计自身的状态。记$b(s)$为智能体位于状态$s$的概率，通过行为$a$和观测$z$我们可以更新智能体位于新的状态$s'$的概率：

$$
\begin{aligned}
b(s') &= P(s' \vert b, a, z) = \sum_s P(s \vert b, a, z) \cdot P(s' \vert b, a, z, s) \\
&= \sum_s b(s) P(s' \vert a, z, s) \\
&= \sum_s b(s) \cdot \frac{P(z \vert s', a, s) P(s' \vert a, s)}{P(z \vert a, s)} \\
&= \frac{\sum_s b(s) O(s', z) T(s, a, s')}{\sum_{s'} \sum_s b(s) O(s', z) T(s, a, s')}
\end{aligned}
$$

<div align=center>
<img src="https://i.imgur.com/Vua9EzY.png?1" width="80%">
<img src="https://i.imgur.com/xGPIeNt.png" width="80%">
</div>

## Value Iteration in POMDP
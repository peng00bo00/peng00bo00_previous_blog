---
layout: article
title: OMSCS-RL课程笔记05-AAA
tags: ["OMSCS", "CS7642-RL"]
key: OMSCS-RL-05
aside:
  toc: true
sidebar:
  nav: OMSCS-RL
---

> 这个系列是Gatech OMSCS 强化学习课程([CS 7642: Reinforcement Learning](https://omscs.gatech.edu/cs-7642-reinforcement-learning))的同步课程笔记。课程内容涉及强化学习算法的理论和相关应用，本节主要讨论不同强化学习算法的性质。
<!--more-->

## Value Iteration

**价值迭代(value iteration, VI)**是我们介绍的第一个强化学习算法。可以证明使用策略迭代算法总是可以在多项式时间内寻找到最优策略：

<div align=center>
<img src="https://i.imgur.com/7fTdf8k.png" width="80%">
</div>

## Linear Programming

另一种求解MDP的方法是使用**线性规划(linear programming)**。根据Bellman方程，价值函数的递归形式为：

$$
V(s) = \max_a \bigg( R(s, a) + \gamma \cdot \sum_{s'} T(s, a, s') \ V (s') \bigg)
$$

显然Bellman方程不是一个线性方程，不过我们可以利用$\max$运算的性质把它转换为一个线性方程。具体来说可以把上式等价地表示为一个约束优化问题：

$$
\begin{aligned}
\min &\sum_s V(s)\\
\text{s.t.} \ V(s) &\geq R(s, a) + \gamma \cdot \sum_{s'} T(s, a, s') \ V (s')
\end{aligned}
$$

这样求解Bellman方程就转换为了一个线性规划问题。此外我们还可以利用对偶性转而求解原始问题的对偶问题：

$$
\begin{aligned}
\max &\sum_s \sum_a q_{s,a} R(s, a)\\
\text{s.t.} \ & 1 + \gamma \sum_s \sum_a q_{s,a} T(s, a, s') = \sum_a q_{s',a}, \forall s' \\
& q_{s,a} \geq 0
\end{aligned}
$$

## Policy Iteration
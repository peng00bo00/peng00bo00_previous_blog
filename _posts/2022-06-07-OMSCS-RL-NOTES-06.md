---
layout: article
title: OMSCS-RL课程笔记06-Messing with Rewards
tags: ["OMSCS", "CS7642-RL"]
key: OMSCS-RL-06
aside:
  toc: true
sidebar:
  nav: OMSCS-RL
---

> 这个系列是Gatech OMSCS 强化学习课程([CS 7642: Reinforcement Learning](https://omscs.gatech.edu/cs-7642-reinforcement-learning))的同步课程笔记。课程内容涉及强化学习算法的理论和相关应用，本节主要讨论奖励函数对强化学习算法的影响。
<!--more-->

奖励函数是强化学习中非常重要的组成部分。实际上奖励函数不仅会影响到算法的收敛速度，而且也会影响最终学习到的策略。

<div align=center>
<img src="https://i.imgur.com/D1oxTyr.png" width="80%">
</div>

## Changing the Reward Function

首先考虑修改奖励函数是否会影响到最终学习到的策略。如果不希望改变学习到的策略，我们对每一步获得的奖励乘以一个正数或者加减一个常数，实际上还有一些非线性的变形方法可以保证学习到的策略不会发生改变。

<div align=center>
<img src="https://i.imgur.com/tfm0KMJ.png" width="80%">
</div>

### Multiplying by a Scalar

最简单的变形方法是对当前的奖励函数乘以一个常数$c \gt 0$：

$$
R'(s, a) = c \cdot R(s, a)
$$

假设原始MDP的价值函数为$Q(s, a)$，

$$
Q(s, a) = R(s, a) + \gamma \cdot \sum_{s'} T(s, a, s') \ \max_{a'} Q(s', a')
$$

可以证明修改奖励函数后得到的价值函数$Q'(s, a)$满足

$$
\begin{aligned}
c \cdot Q(s, a) &= c \cdot R(s, a) + \gamma \cdot \sum_{s'} T(s, a, s') \ \max_{a'} c \cdot Q(s', a') \\
&= Q'(s, a)
\end{aligned}
$$

### Adding a Scalar

同样地，很容易证明在当前奖励函数上加减一个常数相当于在价值函数进行加减：

$$
R'(s, a) = R(s, a) + c
$$

$$
\begin{aligned}
Q(s, a) + \frac{c}{1-\gamma} &= R(s, a) + c + \gamma \cdot \sum_{s'} T(s, a, s') \ \max_{a'} Q(s', a') \ + \frac{c}{1-\gamma} \gamma \\
&= \bigg[ R(s, a) + c \bigg] + \gamma \cdot \sum_{s'} T(s, a, s') \ \max_{a'} \bigg[ Q(s', a') + \frac{c}{1-\gamma} \bigg] \\
&= Q'(s, a)
\end{aligned}
$$

## Reward Shaping

### Potential-Based Shaping

### Q-Learning with Potentials
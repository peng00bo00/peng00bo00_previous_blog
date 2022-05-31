---
layout: article
title: OMSCS-RL课程笔记04-Convergence
tags: ["OMSCS", "CS7642-RL"]
key: OMSCS-RL-04
aside:
  toc: true
sidebar:
  nav: OMSCS-RL
---

> 这个系列是Gatech OMSCS 强化学习课程([CS 7642: Reinforcement Learning](https://omscs.gatech.edu/cs-7642-reinforcement-learning))的同步课程笔记。课程内容涉及强化学习算法的理论和相关应用，本节讨论TD learning的收敛性。
<!--more-->

## Bellman Equations with Actions

对于不考虑智能体决策行为的情况，Bellman方程给出了价值函数的递归关系：

$$
V(s) = R(s) + \gamma \sum_{s'} T(s, s') V(s')
$$

而TD(0)则给出了价值函数的在线估计方法：

$$
V_t(s_{t-1}) = V_{t-1}(s_{t-1}) + \alpha_t \bigg[ r_t + \gamma V_{t-1} (s_t) - V_{t-1} (s_{t-1}) \bigg]
$$

我们把TD(0)的思路拓展到需要进行决策的情况，可以得到Q函数的更新算法：

$$
Q(s, a) = R(s, a) + \gamma \cdot \sum_{s'} T(s, a, s') \ \max_{a'} Q(s', a')
$$

$$
Q_t(s_{t-1}, a_{t-1}) = Q_{t-1}(s_{t-1}, a_{t-1}) + \alpha_t \bigg[ r_t + \gamma \cdot \max_{a'} Q_{t-1}(s_{t-1}, a') - Q_{t-1}(s_{t-1}, a_{t-1}) \bigg]
$$

<div align=center>
<img src="https://i.imgur.com/lxnLPjy.png" width="80%">
</div>

## Bellman Operator

实际上我们可以使用算子的角度来认识Bellman方程。我们定义Bellman算子$B$是一个价值函数到价值函数的映射：

$$
[B \ Q] (s, a) = R(s, a) + \gamma \cdot \sum_{s'} T(s, a, s') \ \max_{a'} Q(s', a')
$$

利用Bellman算子，我们可以重写Bellman方程和TD(0)更新：

$$
Q^* = B \ Q^*
$$

$$
Q_t = B \ Q_{t-1}
$$

## Contraction Mapping

Bellman算子的一个重要性质是它是一个**压缩映射(contraction mapping)**。所谓压缩映射是指对于任意函数$F$和$G$，存在$0 \leq \gamma \lt 1$使得对于算子$B$满足：

$$
\Vert B \ F - B \ G \Vert_\infty \leq \gamma \Vert F - G \Vert_\infty
$$

直观理解，压缩映射会不断减少两个函数之间的距离。压缩映射有很多有用的性质，比如说对于压缩映射$B$一定存在一个唯一的函数$F^*$满足方程：

$$
B \ F^* = F^*
$$

同时，我们可以从任意函数$F$开始利用$B$进行迭代，最终一定能收敛到$F^*$上：

$$
F_t = B \ F_{t-1} \Rightarrow F_t \rightarrow F^*
$$

<div align=center>
<img src="https://i.imgur.com/Y85m69p.png" width="80%">
</div>

容易验证Bellman算子满足压缩映射的定义：

$$
\begin{aligned}
\Vert B \ Q_1 - B \ Q_2 \Vert_\infty &= \max_{s, a} \bigg\vert \gamma \sum_{s'} T(s, a, s') \bigg[ \max_{a'} Q_1(s', a') - \max_{a'} Q_2(s', a') \bigg] \bigg\vert \\
&\leq \gamma \max_{s'} \vert \max_{a'} Q_1(s', a') - \max_{a'} Q_2(s', a') \vert \\
&\leq \gamma \Vert  Q_1 - Q_2 \Vert_\infty
\end{aligned}
$$

<div align=center>
<img src="https://i.imgur.com/OTjD0FM.png" width="80%">
</div>
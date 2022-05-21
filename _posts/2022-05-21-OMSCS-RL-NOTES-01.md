---
layout: article
title: OMSCS-RL课程笔记01-Introduction
tags: ["OMSCS", "CS7642-RL"]
key: OMSCS-RL-01
aside:
  toc: true
sidebar:
  nav: OMSCS-RL
---

> 这个系列是Gatech OMSCS 强化学习课程([CS 7642: Reinforcement Learning](https://omscs.gatech.edu/cs-7642-reinforcement-learning))的同步课程笔记。课程内容涉及强化学习算法的理论和相关应用，本节主要强化学习的概念。
<!--more-->

## Decision Making & Reinforcement Learning

在机器学习课程中我们介绍过各种机器学习算法大致可以分为三类：**监督学习(supervised learning)**、**无监督学习(unsupervised learning)**以及**强化学习(reinforcement learning)**。其中监督学习的目标是从数据中学习到一个映射$y=f(x)$，无监督学习的目标是学习数据分布上的结构，而强化学习的目标同样是学习一个映射$y=f(x)$。但和监督学习不同的是，在强化学习中的目标$f(x)$并不是直接从数据进行学习的。在强化学习中有所谓**环境(environment)**的概念，在每一时刻**智能体(agent)**会根据它当前的**状态(state)**与环境进行互动，同时环境也会给予智能体一个反馈信号称为**奖励(reward)**。我们希望智能体能够学习到一个决策函数$f(x)$从而最大化环境给予的奖励。

## Markov Decision Process

**Markov决策过程(Markov decision process, MDP)**是强化学习的基本理论框架。一个标准的MDP包含以下元素：

1. **状态(state)**表示智能体所处的状态$s$；
2. **模型(model)**表示智能体从状态$s$执行动作$a$后转移到状态$s'$的概率，即$T(s, a, s') \sim P(s' \vert s, a)$；
3. **动作(action)**表示智能体可以执行的行为$a$；
4. **奖励(reward)**表示环境给予智能体的奖励信号，在不同算法中它可以记为$R(s)$、$R(s, a)$或者$R(s, a, s')$等；
5. **策略(policy)**表示智能体进行决策的函数，它将状态$s$映射为一个动作$a$即$a = \pi(s)$，其中具有最大长期奖励的策略称为最优策略(optimal policy)，记为$\pi^*$；

实际上状态、模型、动作以及奖励定义了整个待求解的问题，而强化学习的目标是求解出这个MDP的最优策略。

## Sequences of Rewards

在强化学习中一种常见的情况是考虑无限长序列的累计奖励：

$$
U(s_0, s_1, ...) = \sum_{t=0}^\infty R(s_t)
$$

在这种情况下的效用是不收敛的，我们也无法基于效用来比较不同策略的好坏。为了处理这种问题我们需要引入折扣系数$0 \leq \gamma \lt 1$对$t$时刻的奖励进行加权，此时的效用可以表示为一个几何级数：

$$
U(s_0, s_1, ...) = \sum_{t=0}^\infty \gamma^t R(s_t)
$$

这样就可以保证效用的收敛性：

$$
U(s_0, s_1, ...) \leq \sum_{t=0}^\infty \gamma^t R_{\max} = \frac{R_{\max}}{1-\gamma}
$$

## Policies

## The Bellman Equations
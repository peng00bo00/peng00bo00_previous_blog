---
layout: article
title: OMSCS-ML课程笔记13-Markov Decision Processes
tags: ["OMSCS", "CS7641-ML"]
key: OMSCS-ML-13
aside:
  toc: true
sidebar:
  nav: OMSCS-ML
---

> 这个系列是Gatech OMSCS 机器学习课程([CS 7641: Machine Learning](https://omscs.gatech.edu/cs-7641-machine-learning))的同步课程笔记。课程内容涉及监督学习、无监督学习和强化学习三个部分，本节开始介绍强化学习的相关内容。
<!--more-->

**强化学习(reinforcement learning)**是机器学习的另一个重要组成部分。在强化学习任务中，我们希望智能体(agent)能够通过和环境的互动来学习到如何进行决策并获得最大收益。

## Markov Decision Processes

强化学习的基本理论框架是**马尔科夫决策过程(Markov decision processes, MDP)**，这里首先介绍一些相关的概念：

- 智能体自身的**状态(state)**用$s$来表示；
- 智能体可以采取一些**行为(action)**来跟外界进行互动，用$a$来表示；
- 当智能体执行了行为$a$后它自身的状态会发生改变，**状态转移(transition)**用$T$来表示$T(s, a, s') = P(s' \vert s, a)$；
- 当智能体的状态发生转移时，外界环境会给予它一定的**回报(reward)**记为$R$。

我们假定系统满足**马尔科夫性(Markovian property)**，即状态转移仅与当前状态有关而与转移的历史无关；此外我们还默认环境是稳定的，它在和智能体的互动中不会发生改变。这样我们可以把智能体和环境的互动过程用下图来表示：

<div align=center>
<img src="https://images.deepai.org/django-summernote/2019-03-19/c8c9f96b-cc21-4d33-8b37-cb810f599e6e.png" width="40%">
</div>

强化学习的目标是得到一个最优的**策略(policy)**使得智能体能够获得尽可能多的回报。所谓"策略"是指行为关于状态的函数$\Pi(s): S \rightarrow A$，它告诉智能体在给定的状态$s$下该如何确定自身的行为。

## Bellman Equation

## Finding Policies
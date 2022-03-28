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

## Algorithms for Solving MDPs

## Deep Q-Learning

## Policy Gradients, Actor-Critic
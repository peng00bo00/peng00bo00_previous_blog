---
layout: article
title: OMSCS-RL课程笔记08-Generalization
tags: ["OMSCS", "CS7642-RL"]
key: OMSCS-RL-08
aside:
  toc: true
sidebar:
  nav: OMSCS-RL
---

> 这个系列是Gatech OMSCS 强化学习课程([CS 7642: Reinforcement Learning](https://omscs.gatech.edu/cs-7642-reinforcement-learning))的同步课程笔记。课程内容涉及强化学习算法的理论和相关应用，本节主要介绍强化学习中的泛化问题。
<!--more-->

## Generalization Idea

强化学习中的**泛化(generalization)**一般是指价值函数在状态空间中的泛化问题。当环境的状态空间过于巨大或者是连续状态空间时，智能体往往无法遍历所有可能的状态。此时我们希望强化学习算法仍然可以很好地估计那些没有经历过的状态，这样的能力即所谓的泛化能力。
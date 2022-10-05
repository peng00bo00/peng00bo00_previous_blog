---
layout: article
title: OMSCS-GA课程笔记04-Max Flow
tags: ["OMSCS", "CS6515-GA"]
key: OMSCS-GA-04
aside:
  toc: true
sidebar:
  nav: OMSCS-GA
---

> 这个系列是Gatech OMSCS 高级算法课程([CS 6515: Intro to Grad Algorithms](https://omscs.gatech.edu/cs-6515-intro-graduate-algorithms))的同步课程笔记。课程内容涉及动态规划、随机算法、分治、图算法、最大流、线性规划以及NP完备等高级算法的设计思想和相关应用，本节主要介绍最大流的相关算法。
<!--more-->

**最大流(max flow)**问题是图上的经典问题。对于有向图G，从节点s向节点t发送数据时每条边都具有一定的容量，显然我们希望最大化发送的数据量而且在每条边上不要超过相应的容量。

<div align=center>
<img src="https://i.imgur.com/qK5OxwP.png" width="80%">
</div>

最大流问题更严格的定义如下：

<div align=center>
<img src="https://i.imgur.com/7iDvGLO.png" width="80%">
<img src="https://i.imgur.com/KbyO2yw.png" width="80%">
<img src="https://i.imgur.com/ltfQPRD.png" width="80%">
</div>

## Ford-Fulkerson Algorithm

## Reference

- [Graphs](https://teapowered.dev/assets/ga-notes.pdf#page=32)
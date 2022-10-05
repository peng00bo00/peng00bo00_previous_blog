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

和其它图上的问题相比，最大流问题的特点在于我们允许图上出现环。

<div align=center>
<img src="https://i.imgur.com/UhjVDCO.png" width="80%">
</div>

不过在最大流问题中我们不允许节点之间存在平行的边，即相互指向的边。如果出现这种情况则可以通过在这一对边上添加一个新节点的方式进行处理。

<div align=center>
<img src="https://i.imgur.com/l8kzaVR.png" width="80%">
</div>

## Ford-Fulkerson Algorithm

求解最大流的基本思想是利用边的容量来构造路径。我们首先初始化每条边的容量为0，然后利用边上剩余的容量来构造一张图并且在这张图上寻找s到t的路径。接着我们计算这条路径上最小的剩余容量，并且把剩余容量填满到路径中。最后不断重复上述过程直到无法构造s到t的路径为止。

<div align=center>
<img src="https://i.imgur.com/WbKTSHq.png" width="80%">
</div>

上述算法的缺陷在于反向的流量，实际上通过反向的流动我们才能最大化流量。

<div align=center>
<img src="https://i.imgur.com/DxSSsTC.png" width="80%">
</div>

因此我们需要考虑反向的流量，即在原始流量的基础上构造**residual network**。在residual network中图的节点与原始图相同，而边的容量取决于原始图上边的流量。

<div align=center>
<img src="https://i.imgur.com/BLtDF9O.png" width="80%">
</div>

这样可以得到Ford-Fulkerson算法：

<div align=center>
<img src="https://i.imgur.com/79EFD7G.png" width="80%">
</div>

Ford-Fulkerson算法的复杂度为$O(mC)$。

<div align=center>
<img src="https://i.imgur.com/06De6CP.png" width="80%">
<img src="https://i.imgur.com/7q9sY8S.png" width="80%">
<img src="https://i.imgur.com/QNB9h4y.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/5Z4VVCj.png" width="80%">
</div>

## Reference

- [Graphs](https://teapowered.dev/assets/ga-notes.pdf#page=32)
---
layout: article
title: OMSCS-GA课程笔记03-Graph Algorithms
tags: ["OMSCS", "CS6515-GA"]
key: OMSCS-GA-03
aside:
  toc: true
sidebar:
  nav: OMSCS-GA
---

> 这个系列是Gatech OMSCS 高级算法课程([CS 6515: Intro to Grad Algorithms](https://omscs.gatech.edu/cs-6515-intro-graduate-algorithms))的同步课程笔记。课程内容涉及动态规划、随机算法、分治、图算法、最大流、线性规划以及NP完备等高级算法的设计思想和相关应用，本节主要介绍图上的相关算法。
<!--more-->

图是一种重要的数据结构，很多现实中的问题都可以抽象为对图的操作。本节课我们首先从图的遍历入手，在介绍图遍历的基础上推导图上的其它算法。

<div align=center>
<img src="https://i.imgur.com/45uIrUu.png" width="80%">
</div>

## Strongly Connected Components

### DFS

**深度优先搜索(depth-first search, DFS)**是对图进行遍历的基本方法。假设图G是一个无向图，通过DFS可以得到图上所有相连的节点。无向图上的DFS算法伪代码如下：

```
DFS(G):
  cc = 0

  for v in V:
    visited[v] = False
  
  for v in V:
    if not visited[v]:
      cc += 1
      Explore(v)

Explore(z):
  ccnum[z] = cc
  visited[z] = True

  for (z, w) in E:
    if not visited[w]:
      Explore(w)
```

DFS的复杂度为$O(n+m)$。

<div align=center>
<img src="https://i.imgur.com/hz0Sfru.png" width="80%">
<img src="https://i.imgur.com/cg2ss85.png" width="80%">
</div>

DFS是很多更高级图算法的基础。除了计算联通节点之外还可以使用DFS来计算联通节点之间的路径，不过此时需要对DFS算法进行一些修改，在进行遍历时使用`prev[v]`来记录当前节点的上一个节点：

```
DFS(G):
  cc = 0

  for v in V:
    visited[v] = False
    prev[v] = None
  
  for v in V:
    if not visited[v]:
      cc += 1
      Explore(v)

Explore(z):
  ccnum[z] = cc
  visited[z] = True

  for (z, w) in E:
    if not visited[w]:
      Explore(w)
      prev[w] = z
```

<div align=center>
<img src="https://i.imgur.com/cBT2xKm.png" width="80%">
</div>

对于有向图我们同样可以使用DFS来计算联通节点。不过此时我们需要引入`pre`和`post`两个数组来记录节点的访问顺序：

```
DFS(G):
  clock = 1

  for v in V:
    visited[v] = False
  
  for v in V:
    if not visited[v]:
      Explore(v)

Explore(z):
  pre[z] = clock
  clock += 1

  visited[z] = True

  for (z, w) in E:
    if not visited[w]:
      Explore(w)
  
  post[z] = clock
  clock += 1
```

<div align=center>
<img src="https://i.imgur.com/qPUkH4f.png" width="80%">
</div>

### Types of Edges

在有向图上使用DFS相当于把图上的节点按照树进行展开。

<div align=center>
<img src="https://i.imgur.com/Wna4aoz.png" width="80%">
</div>

根据`pre`和`post`两个数组上记录的值可以对原始图上的边进行分类：对于有向边`(z, w)`，树上的反向边会出现`post[z] < post[w]`，而其它情况下则满足`post[z] > post[w]`。

<div align=center>
<img src="https://i.imgur.com/wfgAMUt.png" width="80%">
</div>

### Topological Sorting

当图G的DFS tree存在反向边时称图上存在环。

<div align=center>
<img src="https://i.imgur.com/4WU5Y7S.png" width="80%">
</div>

如果有向图G上没有环则称其为一个**有向无环图(directed acyclic graph, DAG)**。对于DAG来说我们可以根据访问顺序对图上的节点进行排序，使得排序后的节点都是从低序号到高序号。具体来说，只需要使用DFS来计算节点顺序然后按照`post`数组的逆序进行排序即可。

<div align=center>
<img src="https://i.imgur.com/6v252OC.png" width="80%">
</div>

这里我们额外需要说明的是拓扑排序后的图上会有两类节点，其中一类没有边进入称为source vertex，还有一类节点没有指向其它节点的边称为sink vertex。对于DAG来说，图上至少有一个source vertex和一个sink vertex。

<div align=center>
<img src="https://i.imgur.com/AqFf4zk.png" width="80%">
</div>

同时注意到source vertex总是具有最大的post数值而sink vertex总是具有最小的post数值，因此另一种可行的拓扑排序算法是不断寻找图上的sink vertex然后删除。

<div align=center>
<img src="https://i.imgur.com/AqFf4zk.png" width="80%">
</div>

### Connectivity

图上的**强联通分量(strongly connected components, SCC)**是图上节点的集合，其中集合内的任意一对节点v和w之间存在相互联通的路径。

<div align=center>
<img src="https://i.imgur.com/ztjYvxm.png" width="80%">
</div>

以下图为例，图上存在5个强连通分量。

<div align=center>
<img src="https://i.imgur.com/2XU5zQj.png" width="80%">
</div>

有向图的一个重要性质在于其SCC之间构成一个DAG，称为metagraph。

<div align=center>
<img src="https://i.imgur.com/iOeu7my.png" width="80%">
</div>

因此在有向图上计算SCC的基本思想在于利用metagraph是一个DAG的性质。我们可以尝试寻找metagraph上的sink SCC然后从图上删除掉，不断重复这样的过程直至图为空。由于选择的是sink SCC，从其中任意一个节点进行访问都只能访问到SCC内的其它节点。

<div align=center>
<img src="https://i.imgur.com/G6qcX2j.png" width="80%">
</div>

那么如何取寻找sink SCC呢？最直观的想法是从`post`数组中选择具有最小数值的那个节点。但遗憾的是具有最小`post`数值的节点不一定位于一个sink SCC中。

<div align=center>
<img src="https://i.imgur.com/GeWMsIQ.png" width="80%">
</div>

实际上具有最大`post`数值的节点一定位于一个source SCC中。

<div align=center>
<img src="https://i.imgur.com/sEvfCZR.png" width="80%">
</div>

因此计算SCC的第一步在于反转图上的边，然后在反转图上寻找source SCC。此时找的source SCC在原始图上是一个sink SCC。

<div align=center>
<img src="https://i.imgur.com/L6P5ANX.png" width="80%">
</div>

这样有向图上计算SCC的算法主要流程为：

1. 反转边的指向得到反转图
2. 在反转图上使用DFS得到节点排序
3. 在原始图上利用排序对节点进行遍历

<div align=center>
<img src="https://i.imgur.com/PXb3YCa.png" width="80%">
<img src="https://i.imgur.com/0uJGpBQ.png" width="80%">
<img src="https://i.imgur.com/iLodiQG.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/x1hJqVe.png" width="80%">
</div>

当然计算SCC算法依赖于最大`post`数值的节点位于source SCC中这一性质。

<div align=center>
<img src="https://i.imgur.com/UKjcCwk.png" width="80%">
<img src="https://i.imgur.com/fdZfGpg.png" width="80%">
</div>

## 2-Satisfiability

## Minimum Spanning Tree

## Reference

- [Graphs](https://teapowered.dev/assets/ga-notes.pdf#page=32)
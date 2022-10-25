---
layout: article
title: OMSCS-GA课程笔记03-Graph Algorithms
tags: ["CS6515-GA", "OMSCS"]
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

### SAT Problem

SCC算法的一个应用是求解**布尔可满足性问题(satisfiability, SAT)**。在SAT问题中有n个布尔变量，我们希望能够找到满足语句要求的变量值：

<div align=center>
<img src="https://i.imgur.com/oi66qd5.png" width="80%">
</div>

从更严格的角度来说，对于包含n个布尔变量和m个从句的语句我们希望能够找到一个对布尔变量的赋值使得语句的布尔值为True。

<div align=center>
<img src="https://i.imgur.com/jm9w1CR.png" width="80%">
</div>

### k-SAT

根据每个从句的规模我们可以定义k-SAT问题，其中每个从句包含最多k个布尔变量。对于k-SAT问题人们已经证明在k大于2的情况下它是[NP-complete](/2022/10/25/OMSCS-GA-NOTES-06.html#3sat)，而对于2-SAT问题则存在多项式复杂度的解法。

<div align=center>
<img src="https://i.imgur.com/bs0xoCX.png" width="80%">
</div>

对于2-SAT问题我们可以简化语句，首先满足只包含1个变量的从句然后从整个语句中删除它。

<div align=center>
<img src="https://i.imgur.com/W8Pq29A.png" width="80%">
</div>

通过不断地简化我们最终会得到一个新的语句。显然两个语句的可满足性是等价的，因此只需要验证新的语句是否是可满足的即可。

<div align=center>
<img src="https://i.imgur.com/uR6qiDX.png" width="80%">
</div>

### Graph of Implications

语句化简后我们可以把它等价地表示为一张图，称为**graph of implications**。具体地，我们把n个变量的布尔取值表示为图上的节点，而m个从句则可以表示为2条对应的边。

<div align=center>
<img src="https://i.imgur.com/yNMISSg.png" width="80%">
</div>

如果语句是可满足的，那么graph of implications上不能存在任意变量$x$到$\bar{x}$的路径，否则会产生矛盾。换句话说，如果$x$和$\bar{x}$位于同一个SCC中，则语句是无法满足的。

<div align=center>
<img src="https://i.imgur.com/OXvX2Gn.png" width="80%">
</div>

### SCC's

这样我们就可以利用SCC的算法来解决2-SAT问题，如果每一对布尔变量都位于不同的SCC中则说明语句是可以满足的。

<div align=center>
<img src="https://i.imgur.com/BSbd4nA.png" width="80%">
</div>

首先我们在图上寻找一个sink SCC，记为$S$。然后满足$S$中的所有条件，从图上删除SCC并不断重复上面的过程。这个算法的缺陷在于没有考虑S的补集$\bar{S}$，当$S$得到满足时$\bar{S}$可能是无法满足的。

<div align=center>
<img src="https://i.imgur.com/wjwNeSz.png" width="80%">
</div>

为了解决这样的问题，我们可以考虑在图上寻找一个source SCC，记为$S'$。然后把$S'$设为False，并且从图上删除$S'$。最后寻找$S'$的补集$\bar{S'}$，其必为一个sink SCC，然后将其设为True即可。

<div align=center>
<img src="https://i.imgur.com/Z5nvgok.png" width="80%">
</div>

### 2-SAT Algorithm

总结一下，利用SCC算法来求解2-SAT问题的方法如下：

<div align=center>
<img src="https://i.imgur.com/tWsP35X.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/zlSxQ7q.png" width="80%">
<img src="https://i.imgur.com/05RJdi8.png" width="80%">
<img src="https://i.imgur.com/Y2hDAv0.png" width="80%">
</div>

## Minimum Spanning Tree

### Greedy Approach

**贪心(greedy)**是经典的算法设计思想，在贪心算法中我们把整个问题分解为若干个子问题然后通过最优化每一个子问题来试图优化原始问题。当然并不是所有的问题都可以使用贪心这样的方法来进行优化，比如说[knapsack问题](/2022/08/23/OMSCS-GA-NOTES-01.html#knapsack)就无法通过贪心来进行求解。

<div align=center>
<img src="https://i.imgur.com/cYqRFpX.png" width="80%">
</div>

### MST Problem

**最小生成树(minimum spanning tree, MST)**是图上的经典问题，我们希望对于无向图G可以找到一个最小的子图来包含原始图的所有节点。显然这个最小的子图一定是一个树结构，称为最小生成树。

<div align=center>
<img src="https://i.imgur.com/SgyiwM6.png" width="80%">
</div>

在介绍计算MST的算法前我们先来回顾一下树这种数据结构的性质。首先树是一个DAG，而且对于包含n个节点的树其边的数量为n-1，同时树上任意两个节点之间有且只有一条路径连接它们。关于树最重要的一条性质是如果一张图的边和节点数满足$\vert E \vert = \vert V \vert - 1$，那么它一定是一棵树。

<div align=center>
<img src="https://i.imgur.com/Tl0RmUX.png" width="80%">
</div>

### Greedy Approach for MST

MST可以使用贪心的思想来进行计算。我们可以不断地在添加图上具有最小权重的边，同时保证生成的图是一棵树即可。这种计算MST的算法称为**Kruskal算法(Kruskal's algorithm)**，它的复杂度为$O(m \log{n})$。

<div align=center>
<img src="https://i.imgur.com/WYYmazs.png" width="80%">
<img src="https://i.imgur.com/ZJvv0Pc.png" width="80%">
</div>

Kruskal算法的正确性则可以使用归纳法来进行证明。

<div align=center>
<img src="https://i.imgur.com/ZaYKVJ3.png" width="80%">
</div>

### Cuts

我们还可以借助**图割(cut)**的概念来处理MST问题。cut是指把图上的节点分为两个集合$S$和$\bar{S}$，其中连接两个集合的边称为cut edge。

<div align=center>
<img src="https://i.imgur.com/2lASuxt.png" width="80%">
</div>

基于cut的概念，Kruskal算法可以理解为不断地寻找当前图上的最小cut edge。

<div align=center>
<img src="https://i.imgur.com/vndNPfm.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/02FNcZr.png" width="80%">
<img src="https://i.imgur.com/FEgdwaZ.png" width="80%">
<img src="https://i.imgur.com/UXHDbG7.png" width="80%">
<img src="https://i.imgur.com/AlAzKMz.png" width="80%">
</div>

### Prim's Algorithm

除了Kruskal算法之外，**Prim算法(Prim's algorithm)**同样是计算MST的经典算法。

<div align=center>
<img src="https://i.imgur.com/3G3NeeJ.png" width="80%">
</div>

## Reference

- [Graphs](https://teapowered.dev/assets/ga-notes.pdf#page=32)
- [最小生成树 Minimum Spanning Trees](https://www.youtube.com/watch?v=KsobpcI3dN0&list=PLvOO0btloRnsbnIIbX6ywvD8OZUTT0_ID&index=5)
- [Prim算法 寻找最小生成树 Prim's Algorithm for Minimum Spanning Trees](https://www.youtube.com/watch?v=GLlIaT_PxVE&list=PLvOO0btloRnsbnIIbX6ywvD8OZUTT0_ID&index=6)
- [Kruskal算法 寻找最小生成树](https://www.youtube.com/watch?v=Z4jm4o2bt28&list=PLvOO0btloRnsbnIIbX6ywvD8OZUTT0_ID&index=7)
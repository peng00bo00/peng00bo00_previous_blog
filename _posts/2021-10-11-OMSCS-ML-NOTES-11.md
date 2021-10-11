---
layout: article
title: OMSCS-ML课程笔记11-Clustering
tags: ["OMSCS", "CS7641-ML"]
key: OMSCS-ML-11
aside:
  toc: true
sidebar:
  nav: OMSCS-ML
---

> 这个系列是Gatech OMSCS 机器学习课程([CS 7641: Machine Learning](https://omscs.gatech.edu/cs-7641-machine-learning))的同步课程笔记。课程内容涉及监督学习、无监督学习和强化学习三个部分，本节主要介绍无监督学习中聚类算法的相关内容。
<!--more-->

从本节开始我们正式进入**无监督学习(unsupervised learning)**的范畴。在监督学习中每个给定的数据点$x$都具有对应一个标签$y$，我们的目标是从数据中学习到一个函数$f$进而推广到全体数据上进行预测；而在无监督学习中我们只具有数据点，我们的目标则是挖掘数据之间的关系。因此在某种意义上监督学习类似于函数拟合，而无监督学习则是对数据进行建模。

**聚类(clustering)**是无监督学习中的基本问题之一。在聚类问题中我们需要把给定的样本划分到不同的簇中，使得相似的样本位于同一个簇。具体来说，对于给定的数据集$X$和距离度量函数$d(x, y)$，聚类算法的目标是获得一个划分函数$P_D(x)$使得位于同一个簇的样本$x$和$y$具有相同的划分$P_D(x) = P_D(y)$。

## Single Linkage Clustering

**Single linkage clustering(SLC)**是典型的层次聚类算法，它的基本流程如下：

1. 将数据集中每个样本都视为一个聚类中心，得到$n$个簇；
2. 将距离最近的两个簇合并成一个新的簇，同时更新其它簇和它的距离$D(X, Y) = \min_{x \in X, y \in Y} d(x, y)$，即簇$X$和簇$Y$的距离为它们两个内部点距离的最小值；
3. 重复第2步直到数据集上的簇数量满足要求。

<div align=center>
<img src="https://upload.wikimedia.org/wikipedia/commons/4/43/Simple_linkage-5S.svg" width="50%">
</div>

SLC有很多有趣的性质：首先SLC是一个确定性的算法，当输入数据集确定时SLC的输出是确定的；其次，如果我们把数据看做是一张图同时把数据之间的距离看做是连接节点的边，SLC算法实际上等价于在图上构造一棵最小生成树。SLC的主要缺陷在于它的复杂度，对于包含$n$个样本的数据集它的时间复杂度为$O(n^3)$：我们需要$O(n)$次循环，同时每个循环需要计算$O(n^2)$次簇距离。

SLC的另一个缺陷在于它忽视了数据之间的结构。以下图为例，假设我们需要将(a)图所示的数据点划分为2类，一个直观的聚类结果是(b)图：左边的圆是一类而右边的把手部分是一类；但使用SLC算法则会得到(c)图：这是由于圆边上的距离都要小于圆的边到内部点的距离，因此在聚类时圆边上的点都会划分为一类并与右边把手相连，而剩下的圆内部点则会划分为另一类。

<div align=center>
<img src="https://i.imgur.com/G9jl8aY.png" width="90%">
</div>

## k-Means


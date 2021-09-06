---
layout: article
title: OMSCS-ML课程笔记04-Instance Based Learning
tags: ["OMSCS", "CS7641-ML"]
key: OMSCS-ML-04
aside:
  toc: true
sidebar:
  nav: OMSCS-ML
---

> 这个系列是Gatech OMSCS 机器学习课程([CS 7641: Machine Learning](https://omscs.gatech.edu/cs-7641-machine-learning))的同步课程笔记。课程内容涉及监督学习、无监督学习和强化学习三个部分，本节主要介绍监督学习中kNN的相关内容。
<!--more-->

## Overview

之前在课程中介绍的各种机器学习算法都是需要通过数据学习到一个模型(函数)来完成分类或是回归的任务，与之相对的instance based learning相关的学习算法则没有显式地学习过程。在instance based learning中我们只需要构建出数据库，然后用新的数据在已有数据库中进行查询进而完成分类和回归的任务。

和其它类型的机器学习算法相比，instance based learning相关的算法更简单同时效率更高。但相应地由于instance based learning算法极度依赖于已有的数据库，和其他类型的算法相比它的泛化性能更差，也更容易收到数据库中噪声的影响，更容易出现过拟合的问题。

## k-NN

instance based learning算法中最出名的是**k-NN算法(k nearest neighbor)**。简单来说当我们使用数据$x$进行查询时，从数据库中选出k个与$x$最接近的样本，然后利用这些样本来求解分类和回归的问题。对于分类问题可以使用这k个样本进行投票，票数最多的类别即为$x$的类别；而对于回归问题则可以使用k个样本的平均值来作为$x$的预测值。

从k-NN算法的流程不难发现如何计算样本间的距离对于算法的性能起着至关重要的作用。常用的距离函数包括欧式距离、Manhattan距离等，在实际应用中一般还会结合一些domain knowledge来设计合适的距离函数。

k值的选择同样会对kNN的结果产生重大影响。当k值比较小时模型会只考虑与输入数据$x$相近的样本，此时模型更容易收到数据库中误差的影响造成过拟合的问题。而当k较大时模型会考虑更多的样本，此时与$x$差距较大的样本也会对输出的结果产生影响从而产生误差。在k取样本数的极端情况下无论什么样输入数据$x$模型都会给出相同的答复，此时的模型是没有任何意义的。在实际应用中通常会使用交叉验证的方法来选择最优的k值。

在大规模高维的数据库中对数据$x$进行查询会极大地影响k-NN的算法效率。最简单的查询方法是进行线性扫描，即依次计算$x$与每一个样本的距离并保留其中最小的k个。显然线性扫描的方法在大规模数据库中会非常低效，在实际应用中更常用的方式是使用**kd树(kd tree)**的数据结构来存储训练数据。当数据均匀分布时可以证明使用kd树进行搜索的平均复杂度是$O(\log n)$，远小于线性扫描的复杂度$O(n)$。

## Bias

## Curse of Dimensionality

## Reference

- 第3章：k邻近法，统计学习方法（第2版）
- [Wikipedia: k-d tree](https://en.wikipedia.org/wiki/K-d_tree)
- [Wikipedia: Curse of dimensionality](https://en.wikipedia.org/wiki/Curse_of_dimensionality#Machine_Learning)
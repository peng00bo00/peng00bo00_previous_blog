---
layout: article
title: OMSCS-ML课程笔记01-Decision Trees
tags: ["OMSCS", "ML"]
key: OMSCS-ML-01
aside:
  toc: true
sidebar:
  nav: OMSCS-ML
---

> 这个系列是Gatech OMSCS 机器学习课程([CS 7641: Machine Learning](https://omscs.gatech.edu/cs-7641-machine-learning))的同步课程笔记。课程内容涉及监督学习、无监督学习和强化学习三个部分，本节主要介绍监督学习中的决策树相关内容。
<!--more-->

## Representation

**决策树(Decision Tree)**是应用最为广泛的机器学习方法之一，通常用于离散变量的分类问题。日常生活中的很多分类问题都可以通过一系列的判断来解决，此时我们的决策过程就可以利用决策树来表示。比如说我们通过天气的状况来判断是否要出去，此时的决策过程就对应着一个决策树。

<div align=center>
<img src="https://i.imgur.com/Lk80vLQ.png" width="50%">
</div>

除此之外决策树可以看做是一系列的if-then规则：从根节点出发的每一条路径都对应着一个决策规则，而叶节点对应规则的结论。对于分类问题我们从根节点出发每次选择一个属性进行判断，然后不断向下移动直到返回所需的结果。

## Decision Tree Learning

### ID3 

### C4.5

### CART

## Inductive Bias

## Other Considerations

### Continuous Attributes

### Stopping Criteria

### Regression

## Reference
- Chapter 3: Decision Tree Learning, [Machine Learning, Tom Mitchell, McGraw Hill, 1997.](http://www.cs.cmu.edu/afs/cs.cmu.edu/user/mitchell/ftp/mlbook.html)
- 第5章：决策树，统计学习方法（第2版）
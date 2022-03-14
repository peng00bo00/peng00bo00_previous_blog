---
layout: article
title: OMSCS-DL课程笔记14-Neural Attention Models
tags: ["OMSCS", "CS7643-DL"]
key: OMSCS-DL-14
aside:
  toc: true
sidebar:
  nav: OMSCS-DL
---

> 这个系列是Gatech OMSCS 深度学习课程([CS 7643: Deep Learning](https://omscs.gatech.edu/cs-7643-deep-learning))的同步课程笔记。课程内容涉及深度学习的基本理论方法以及它在计算机视觉、自然语言处理以及决策理论等领域中的应用，本节主要介绍深度学习中的注意力模型。
<!--more-->

## Softmax and Preview of Attention

**注意力模型(attentaion model)**是最近几年深度学习领域非常火爆的模型。简单来说注意力模型的核心是为输入分配不同的计算权重，权重的大小一般可由softmax函数来动态确定。因此在介绍注意力模型的原理之前我们先回顾一下softmax函数。

<div align=center>
<img src="https://i.imgur.com/OY3k0MU.png" width="80%">
</div>

### Review of Softmax Function

softmax函数是在多分类问题中非常常用的函数，它可以把给定的向量转换成一个概率分布。

<div align=center>
<img src="https://i.imgur.com/gqKUD0q.png" width="80%">
<img src="https://i.imgur.com/NMT6YyU.png" width="80%">
<img src="https://i.imgur.com/tqQ7GyI.png" width="80%">
</div>

### Softmax and Index Selection

在分类问题中我们一般会选择概率最大的索引作为最终的类别。但需要注意的是softmax的整个计算过程是可微的，而且我们也可以对softmax进行采样来获取类别标签。

<div align=center>
<img src="https://i.imgur.com/YS6wgwr.png" width="80%">
<img src="https://i.imgur.com/Xjg4KVW.png" width="80%">
<img src="https://i.imgur.com/lPwdFa3.png" width="80%">
</div>

### Selecting a Vector from a Set

在很多应用场景中我们需要根据一个查询向量$q$来获取给定向量集合$U=\{ u_1, ..., u_N\}$中最接近的一个向量。最直观的做法是把$q$和$U$中的每一个向量做内积然后选择其中最大的那个作为输出；而利用softmax函数我们也可以对$U$计算概率来实现类似的功能。这种使用softmax函数来计算权重的方法称为**softmax注意力(softmax attention)**。

<div align=center>
<img src="https://i.imgur.com/tmeLaHy.png" width="80%">
<img src="https://i.imgur.com/6M9pYke.png" width="80%">
<img src="https://i.imgur.com/uVDwCZd.png" width="80%">
<img src="https://i.imgur.com/lq37Ebh.png" width="80%">
</div>

### Softmax Attention and MLP Outputs

在softmax attention中我们会把softmax后的结果作为中间隐层，然后利用$U$的概率分布实现不同的功能。

<div align=center>
<img src="https://i.imgur.com/nJ7RElp.png" width="80%">
</div>

## Attention

## Transformers
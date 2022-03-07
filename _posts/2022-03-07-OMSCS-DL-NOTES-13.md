---
layout: article
title: OMSCS-DL课程笔记13-Embeddings
tags: ["OMSCS", "CS7643-DL"]
key: OMSCS-DL-13
aside:
  toc: true
sidebar:
  nav: OMSCS-DL
---

> 这个系列是Gatech OMSCS 深度学习课程([CS 7643: Deep Learning](https://omscs.gatech.edu/cs-7643-deep-learning))的同步课程笔记。课程内容涉及深度学习的基本理论方法以及它在计算机视觉、自然语言处理以及决策理论等领域中的应用，本节主要介绍各种嵌入技术。
<!--more-->

**嵌入(embedding)**的目的是获得不同对象的结构化表示。在深度学习中embedding一般是指通过一个神经网络来将不同类型的对象向量表示，embedding的对象可以是词、图片、句子、概念等等。一个好的embedding需要将具有相似属性的对象映射到相邻的空间中，因此embedding问题的核心是如何训练神经网络来获得合适的embedding向量。

<div align=center>
<img src="https://i.imgur.com/ZIPMwWv.png" width="80%">
<img src="https://i.imgur.com/uf1ba4q.png" width="80%">
</div>

## Word Embeddings

**词嵌入(word embedding)**是NLP中的一个基础方法。它的基本思想是每个单词的意思是由它的上下文语境来决定的，因此可以通过单词的上下文来建立词向量。

<div align=center>
<img src="https://i.imgur.com/7cZY7xb.png" width="80%">
</div>

词嵌入并不是一个特别新的技术，实际上早在03年就提出了通过大量语料训练词向量的方法。不过词嵌入的大规模应用则要归功于13年提出的**word2vec**方法。

<div align=center>
<img src="https://i.imgur.com/eN2HULc.png" width="80%">
</div>

在介绍word2vec前我们简单了解一下传统的词向量是如何训练的。它的基本思路是把词向量的训练转换成一个二分类问题：我们可以把一个句子中出现的单词看做是正样本，把随机替换单词后的句子看做负样本，然后通过SVM来训练得到词向量。

<div align=center>
<img src="https://i.imgur.com/Tiuwv82.png" width="80%">
</div>

### Word2vec

目前更加流行的词嵌入方法是基于word2vec来训练词向量。word2vec使用skip-gram的方式来选取正样本，即对于中心词$w_t$把它前后相邻$m$距离内的词作为正样本。模型的目标在于给定中心词$w_t$的条件下预测窗口内单词出现的概率$P(w_{t+i} \vert w_t)$。

<div align=center>
<img src="https://i.imgur.com/oY5Z1tz.png" width="80%">
<img src="https://i.imgur.com/V1DAv7E.png" width="80%">
</div>

在训练word2vec时我们只需要通过滑窗的方式来遍历语料，然后最大化正样本的联合概率即可，这种方式等价于最小化似然函数的负对数损失。

<div align=center>
<img src="https://i.imgur.com/Qc7vNEF.png" width="80%">
</div>

### Negative Sampling

word2vec使用了softmax函数来计算正样本的概率。对于中心词$w_t$和上下文单词$w_{t+j}$，这一对单词的倾向性由词向量的内积给出。因此在给定中心词$w_t$的条件下出现单词$w_{t+j}$的概率$P(w_{t+j} \vert w_t)$可以由softmax函数来计算，其中分母需要对所有可能的单词对进行求和。

<div align=center>
<img src="https://i.imgur.com/T2S6W01.png" width="80%">
</div>

显然直接计算分母的代价过于巨大，实践中更常用的方法是通过**负样本采样(negative sampling)**来进行训练。在构造负样本时可以通过随机采样的方式选取正样本$k$倍的随机词来取代上下文词，然后训练一个二分类模型来获得最终所需的词向量。此时整个训练过程相当于最大化正样本出现的概率同时最小化负样本出现的概率。

<div align=center>
<img src="https://i.imgur.com/1yawVC0.png" width="80%">
</div>

当然除了word2vec之外还有很多其它的词嵌入技术。

<div align=center>
<img src="https://i.imgur.com/sDfZMHO.png" width="80%">
</div>

### Evaluation

得到词向量之后我们还需要去评估词向量的性能。目前词向量的平均方法包括intrinsic和extrinsic两类，其中intrinsic是在给定的任务上计算性能指标而extrinsic则是在真实的任务上进行评价。

<div align=center>
<img src="https://i.imgur.com/NPbTjMu.png" width="80%">
</div>

一般来说extrinsic的计算代价会比较大，因此目前最常用的评价方法仍然是intrinsic相关的方法。intrinsic方法在评估词向量时会使用analogy test，即测试具有相似概念的两对单词它们的距离是否相似。具体来说我们可以选择man和woman这一对单词并且计算它们词向量空间上的距离，然后把这个距离作用在单词king上并寻找和该点最接近的单词。如果找到的单词是queen则说明词向量学习到了类比的性质。

<div align=center>
<img src="https://i.imgur.com/DMVYXEo.png" width="80%">
</div>

## Graph Embeddings

## world2vec

## Additional Topics
---
layout: article
title: OMSCS-DL课程笔记12-Language Models
tags: ["OMSCS", "CS7643-DL"]
key: OMSCS-DL-12
aside:
  toc: true
sidebar:
  nav: OMSCS-DL
---

> 这个系列是Gatech OMSCS 深度学习课程([CS 7643: Deep Learning](https://omscs.gatech.edu/cs-7643-deep-learning))的同步课程笔记。课程内容涉及深度学习的基本理论方法以及它在计算机视觉、自然语言处理以及决策理论等领域中的应用，本节主要介绍语言模型。
<!--more-->

## Modeling Language

**语言模型(language models)**是**自然语言处理(natural language processing, NLP)**的重要技术之一。通过语言模型我们可以计算任意一个给定句子出现的概率，也可以比较不同句子出现的可能性。

<div align=center>
<img src="https://i.imgur.com/T6anuxY.png" width="80%">
</div>

严格来说语言模型的目标是计算给定词序列的联合概率，它等价于对序列中每个词的条件概率进行累乘。

<div align=center>
<img src="https://i.imgur.com/GiMu8Ul.png" width="80%">
</div>

语言模型在日常生活中已经有了大量的应用：从输入法的自动联想到语音识别乃至文本的语法检查，这些技术的背后都有语言模型作为基础。

<div align=center>
<img src="https://i.imgur.com/oas29ET.png" width="80%">
</div>

需要说明的一点是尽管语言模型是定义在词序列的联合概率上，但在实际应用中语言模型往往会定义为某个给定条件$c$下的联合概率。根据不同的应用场景，$c$可以表示话题、文档、语种等等不同的条件。

<div align=center>
<img src="https://i.imgur.com/igJVL2A.png" width="80%">
<img src="https://i.imgur.com/7nbPFvX.png" width="80%">
</div>

## Recurrent Neural Networks

### Sequence Modeling

为了处理这种序列数据人们开发出了**循环神经网络(Recurrent Neural Networks, RNN)**，它的典型应用包括语音识别、情感分析、话题分类等。

<div align=center>
<img src="https://i.imgur.com/YHZE4qn.png" width="80%">
</div>

### How to Feed Words to an RNN?

RNN的大部分应用都与文本有关，因此在继续介绍RNN之前首先需要考虑如何对文本进行建模。最简单的建模方法是首先建立一个词典，然后把每个词都转换成一个one-hot vector进行表示。在后面的课程中会陆续介绍更高级的词向量表示方法。

<div align=center>
<img src="https://i.imgur.com/UGFV8ze.png" width="80%">
</div>

### Modeling Sequences with MLPs

有了词向量后就需要考虑如何把词向量构成的序列送入神经网络中。以情感分析为例，我们可以设计一个全连接网络，网络的输入为词向量构成的序列而输出为正向情感或负向情感。

<div align=center>
<img src="https://i.imgur.com/rIyrLC8.png" width="80%">
</div>

而这种全连接网络的缺陷在于它只能处理固定长度的序列，如果句子的长度发生改变就不能再使用这个网络了。

<div align=center>
<img src="https://i.imgur.com/t9sgOUg.png" width="80%">
</div>

总结一下，传统的全连接网络无法适应变长的序列作为输入，也无法产生序列形式的输出。同时全连接网络也无法捕捉序列的时序特性，因此不适合序列形式的任务。

<div align=center>
<img src="https://i.imgur.com/SOaMl5V.png" width="80%">
</div>

### Recurrent Neural Networks

接下来我们开始介绍能够处理序列数据的RNN模型。严格来说RNN是指一类处理序列类型数据的神经网络，它们的特点是在$t$时刻接收输入$x_t$以及上一时刻隐状态$h_{t-1}$作为输入，然后更新当前时刻的隐状态$h_t$。

<div align=center>
<img src="https://i.imgur.com/cGWEeyU.png" width="45%">
</div>

得到隐状态后就可以利用隐状态(序列)执行下游的不同任务。

<div align=center>
<img src="https://i.imgur.com/liEeq9H.png" width="80%">
</div>

### Backpropagation Through Time

需要说明的是由于RNN在计算上是有时序依赖的，在进行反向传播时需要从后向前按照计算顺序的反向来计算导数。显然这种计算方式在序列比较长的情况下会十分低效，因此在RNN的训练过程中往往还会对最大时间进行截断。

<div align=center>
<img src="https://i.imgur.com/O3aAPqT.png" width="80%">
</div>

### Vanilla (Elman) RNN

标准RNN的计算方式与全连接网络没有明显差异，只不过需要同时考虑序列数据$x_t$以及上一时刻隐状态$h_{t-1}$两个输入。

<div align=center>
<img src="https://i.imgur.com/AzA6gvo.png" width="80%">
</div>

然而这种形式的RNN容易出现**梯度消失(vanishing gradients)**或是**梯度爆炸(exploding gradients)**的问题。如果梯度的模大于1，在反向传播时会使得前面的梯度发散；而如果梯度的模小于1，则会使前面的梯度趋于0。

<div align=center>
<img src="https://i.imgur.com/ISc7A37.png" width="80%">
</div>

### Long Short-Term Memory (LSTM) Networks

为了克服这个缺陷人们又开发出了**长短记忆网络(long short-term memory networks, LSTM)**。LSTM包含两个隐状态$h_t$和$c_t$，同时还引入了4种不同的门控制输入。

<div align=center>
<img src="https://i.imgur.com/Ws60YOD.png" width="80%">
</div>

LSTM的正向计算过程可参见下图。

<div align=center>
<img src="https://i.imgur.com/hhCEzSP.png" width="80%">
</div>

## RNN Language Model

## Masked Language Models

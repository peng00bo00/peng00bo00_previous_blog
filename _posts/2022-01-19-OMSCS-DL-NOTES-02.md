---
layout: article
title: OMSCS-DL课程笔记02-Neural Networks
tags: ["OMSCS", "CS7643-DL"]
key: OMSCS-DL-02
aside:
  toc: true
sidebar:
  nav: OMSCS-DL
---

> 这个系列是Gatech OMSCS 深度学习课程([CS 7643: Deep Learning](https://omscs.gatech.edu/cs-7643-deep-learning))的同步课程笔记。课程内容涉及深度学习的基本理论方法以及它在计算机视觉、自然语言处理以及决策理论等领域中的应用，本节主要介绍神经网络的基本知识。
<!--more-->

## Neural Network View of a Linear Classifier

**线性分类器(linear classifier)**是最简单的机器学习模型之一，它通过一个线性变换将输入$X$映射为输出$y$，同时我们还需要一个损失函数来对它进行训练。

<div align=center>
<img src="https://i.imgur.com/uzlx5J8.png" width="80%">
</div>

而简单的神经网络和线性分类器具有相似的结构，每个**神经元(neuron)**接收来自其它神经元的信号并进行组合，如果累计的信号超过一定的阈值则会激活，然后向下一层的神经元发射信号。不过激活的过程往往具有一定的非线性，比如说可以利用sigmoid函数来表示神经元激活后发射的信号。

<div align=center>
<img src="https://i.imgur.com/c0tK5gL.png" width="80%">
<img src="https://i.imgur.com/5Uc12vU.png" width="80%">
</div>

在计算机中，我们通过矩阵乘法来表示相互连接的神经元发射接收信号的过程。神经元接收信号并判断是否激活可以通过权重矩阵$W$和偏置向量$b$来描述。我们把神经元这样的计算封装成一个层，称为**全连接层(fully connected layer)**。

<div align=center>
<img src="https://i.imgur.com/eMMoZ1O.png" width="80%">
</div>

我们还可以通过一张图来表示神经网络：每个神经元对应层输入/输出层的一个节点，神经元之间的连接则构成了图的边。同时不难发现，基本的线性分类器等价于将输入层和输出层直接相连的神经网络，当然还需要去除掉输出层的激活函数。

<div align=center>
<img src="https://i.imgur.com/tBssqP0.png" width="80%">
</div>

如果把更多的层组合到一起就得到了通常意义下的"神经网络"，其中输入层和输出层直接的称为**隐层(hidden layer)**。在大多数情况下统计神经网络的层数都不包含输入层，因此最基本的神经网络模型是仅包含一个隐层的双层神经网络。

<div align=center>
<img src="https://i.imgur.com/9qsFaya.png" width="80%">
</div>

显然增加隐层的数量可以提高神经网络的表达能力，但实际上简单的三层神经网络就足以描述任何连续的函数，这称为**通用逼近定理(universal approximation theorem)**。需要说明的是尽管理论上三层的神经网络可以近似任何形式的连续函数，对于复杂的情况可能需要指数级或是更多数量的神经元才能进行近似，同时训练这样的大型网络也往往是更加困难的。因此层数更深的网络要比神经元更多的网络有着更加广泛的应用。

<div align=center>
<img src="https://i.imgur.com/oalCB8z.png" width="80%">
</div>

## Computation Graphs

## Backpropagation

## Automatic Differentiation

## Vectorization and Jacobians

## Reference

- [Wikipedia: Universal approximation theorem](https://en.wikipedia.org/wiki/Universal_approximation_theorem)
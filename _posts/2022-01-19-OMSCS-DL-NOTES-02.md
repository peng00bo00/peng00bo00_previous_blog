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

我们不仅可以为神经网络添加全连接层，理论上任意可导的函数都可以添加到网络中。同时，在模型的末端还需要添加一个可导的损失函数以便训练网络。

<div align=center>
<img src="https://i.imgur.com/9yUOxDc.png" width="80%">
</div>

对于复杂的模型，我们还需要关注如何前向计算损失函数以及如何计算损失函数对于每一层参数的导数。

<div align=center>
<img src="https://i.imgur.com/cdbpq9z.png" width="80%">
</div>

为了开发出通用的算法，我们需要把整个模型看做是一张**计算图(computation graph)**。

<div align=center>
<img src="https://i.imgur.com/HMV1b0m.png" width="80%">
</div>

一些函数的计算图表示如下：

<div align=center>
<img src="https://i.imgur.com/eSjWbdS.png" width="40%">
<img src="https://i.imgur.com/SmzDlVE.png" width="43%">
</div>

## Backpropagation

对于给定的计算图，模型的训练包括**前向计算(forward pass)**和**反向计算(backward pass)**两个步骤。在前向计算中，我们把数据带入到图上的输入节点并依次计算节点的输出，然后在反向计算中从损失函数出发从后向前计算损失函数的导数。这个算法称为**反向传播(backpropagation)**算法。

<div align=center>
<img src="https://i.imgur.com/r9YNsd6.png" width="80%">
</div>

### Forward Pass

前向计算的过程比较简单，我们只需要按照节点的拓扑顺序从前到后计算节点输出即可。不过在进行前向计算时可能会保存一些中间结果以方便反向计算时计算导数。

<div align=center>
<img src="https://i.imgur.com/rxOAwDW.png" width="80%">
</div>

### Backward Pass

在进行反向计算时我们需要计算损失函数关于每一层参数的导数。从模型的最后一层开始，首先计算损失函数对于输出层的导数$\frac{\partial L}{\partial h^l}$、$\frac{\partial L}{\partial W}$，并把输入项的导数$\frac{\partial L}{\partial h^l}$传给上一层。

<div align=center>
<img src="https://i.imgur.com/KY7B6oF.png" width="80%">
</div>

然后考虑损失函数关于其它层的导数。实际上我们不会直接计算损失函数对于某一层的导数，而是首先计算该层的输出关于输入以及参数的导数$\frac{\partial h^l}{\partial h^{l-1}}$、$\frac{\partial h^l}{\partial W}$。由于计算图上每一层都是可导的，我们可以解析地计算这些局部导数。

<div align=center>
<img src="https://i.imgur.com/X9IQUFw.png" width="80%">
</div>

得到局部导数后再结合**链式法则(chain rule)**将后一层计算的导数乘以当前层的局部导数就可以得到损失函数关于当前层的导数。

<div align=center>
<img src="https://i.imgur.com/AloXoaO.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/gD9Wh6x.png" width="80%">
</div>

这样从后向前依次计算就得到了损失函数关于模型每一层的导数。

<div align=center>
<img src="https://i.imgur.com/N1VW4fN.png" width="80%">
</div>

### Update with Gradients

得到导数后再结合梯度优化算法就可以更新模型的参数。综合以上步骤可以发现，反向传播算法的本质就是利用链式法则和计算图来计算损失函数关于模型参数的导数。

<div align=center>
<img src="https://i.imgur.com/ZqGeoDT.png" width="80%">
</div>

## Automatic Differentiation

## Vectorization and Jacobians

## Reference

- [Wikipedia: Universal approximation theorem](https://en.wikipedia.org/wiki/Universal_approximation_theorem)
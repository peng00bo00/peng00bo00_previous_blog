---
layout: article
title: OMSCS-DL课程笔记03-Optimization of Deep Neural Networks
tags: ["OMSCS", "CS7643-DL"]
key: OMSCS-DL-03
aside:
  toc: true
sidebar:
  nav: OMSCS-DL
---

> 这个系列是Gatech OMSCS 深度学习课程([CS 7643: Deep Learning](https://omscs.gatech.edu/cs-7643-deep-learning))的同步课程笔记。课程内容涉及深度学习的基本理论方法以及它在计算机视觉、自然语言处理以及决策理论等领域中的应用，本节主要介绍深度学习中的优化算法。
<!--more-->

## Architectural Considerations

在深度学习中模型的结构对于最终的性能起着至关重要的作用。在设计网络结构时一般需要考虑不同的数据类型和数据自身的特征，同时还要考虑反向传播时梯度传播的形式以免在训练时产生问题。

<div align=center>
<img src="https://i.imgur.com/5Qo5RFQ.png" width="80%">
</div>

### Linear and Non-Linear Modules

根据计算的形式我们可以把模型中的层分为线性层和非线性层两类。其中线性层是指对输入数据进行线性变换，典型的例子是使用矩阵乘法来表示全连接层；而非线性层则表示对输入数据进行非线性变换，典型的非线性层是网络的激活函数层。需要注意的是线性层的组合仍然是一个线性层，因此非线性层对于提升网络的性能至关重要。

<div align=center>
<img src="https://i.imgur.com/hMmXFMH.png" width="80%">
</div>

### Analysis of Non-Linear Function

接下来我们介绍一些常用的非线性层(激活函数)以及它们的性质。

<div align=center>
<img src="https://i.imgur.com/aDPI60G.png" width="80%">
</div>

#### Sigmoid Function

sigmoid函数是传统神经网络最常用的激活函数，它的特点是能够将任意输入数值映射到(0, 1)区间上。sigmoid函数的缺陷在于当输入数值很大或是很小的时候会出现**饱和(saturation)**的现象，即局部的导数会趋于0容易产生模型无法训练的问题。除此之外sigmoid函数在计算时还涉及对指数函数的运算，因此它的计算效率相对较低。

<div align=center>
<img src="https://i.imgur.com/1zZ2fcX.png" width="80%">
</div>

#### Tanh Function

tanh函数也是传统神经网络常用的一种激活函数。类似于sigmoid，tanh会将输入数值映射到(-1, 1)区间上，而且当函数值较大或较小的时候也会出现饱和的问题。

<div align=center>
<img src="https://i.imgur.com/Jku5UHt.png" width="80%">
</div>

#### Rectified Linear Unit

ReLU函数是现代神经网络最常用的激活函数之一。它会抑制输入数据小于0的部分并将它们映射为0，而对于大于0的部分则保持不变。因此ReLU函数没有饱和的问题，同时在计算时只涉及比较大小它的计算效率要比sigmoid和tanh高得多。

<div align=center>
<img src="https://i.imgur.com/NaaEaHy.png" width="80%">
</div>

#### Leaky ReLU

ReLU函数的缺陷在于反向传播时它会将输入数据小于0的部分导数映射为0。为了解决这样的问题人们开发出了Leaky ReLU这种激活函数，它通过一个可学习参数$\alpha$来对数据进行线性变换。Leaky ReLU在计算时的开销要稍大于ReLU，但仍然是非常高效的。

<div align=center>
<img src="https://i.imgur.com/XqamkgT.png" width="80%">
</div>

最后需要说明的是目前不存在所谓"最好"的激活函数，在实践中一般需要根据不同的任务类型对不同的激活函数进行调试来进行选择。在大多数情况下ReLU函数都具有比较好的性能，而sigmoid函数由于存在饱和的问题因此往往只在需要对数据进行规范化时才会使用。

## Initialization

## Preprocessing, Normalization, and Augmentation

## Optimizers

## Regularization

## Data Augmentation

## The Process of Training Neural Networks
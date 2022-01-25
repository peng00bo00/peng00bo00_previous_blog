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

在训练模型前我们还需要为模型赋予一定的初值，这样的过程称为**初始化(initialization)**。初始化对于模型的训练过程有着重要的影响，一个好的初始化不仅可以加快模型的训练过程，还往往会提升模型最终的性能

<div align=center>
<img src="https://i.imgur.com/EBt3z6M.png" width="80%">
</div>

### A Poor Initialization

一个不好的初始化是将模型的所有参数初始化为一个常数(比如说0)，在这种情况下模型会出现退化的问题。具体来说在进行反向传播时每一个节点得到的梯度都是相同的，因此模型在更新时所有的参数都会更新为相同的值。显然这种情况下模型的性能不会很好。

<div align=center>
<img src="https://i.imgur.com/fVHh6Er.png" width="80%">
</div>

### Gaussian/Normal Initialization

因此更加常用的初始化方法是进行随机初始化，比如说利用均匀分布或是正态分布来初始化参数。这样初始化会使模型参数都分布在一个比较小的区间上，这意味着模型对于不同类型的特征没有明显的偏好，也即所有的输入特征都是相同重要的。

<div align=center>
<img src="https://i.imgur.com/NMZLcxE.png" width="80%">
</div>

还需要说明的是深层网络对于模型的初始化十分敏感。研究发现随着网络层数的增加每一层输出的标准差会不断缩小，这就会导致反向传播时浅层的参数获得的梯度比较小使得训练大型神经网络更加困难。而如果一味地增加初始化的值则容易导致饱和的问题，同样无法训练大型的神经网络。

<div align=center>
<img src="https://i.imgur.com/97M2VGh.png" width="80%">
</div>

### Xavier Initialization

为了解决这样的问题人们提出了**Xavier初始化(Xavier initialization)**，它的思想是通过调整初始化参数使得每一层的输入和输出都具有类似的分布。

<div align=center>
<img src="https://i.imgur.com/QpsUES9.png" width="80%">
</div>

Xavier初始化利用($-\frac{\sqrt{6}}{\sqrt{n_j + n_{j+1}}}$, $\frac{\sqrt{6}}{\sqrt{n_j + n_{j+1}}}$)上的均匀分布来进行初始化。在实践中人们还发现只需要对正态分布初始化稍作变换也能够达到类似的效果。

<div align=center>
<img src="https://i.imgur.com/QyLt38i.png" width="80%">
</div>

## Normalization

### Preprocessing

### Batch Normalization

## Optimizers

### Adding Momentum

### Adagrad

### RMSProp

### Adam

### Learning Rate Schedules

## Regularization

### Dropout

## Data Augmentation

## Training Neural Networks
---
layout: article
title: OMSCS-DL课程笔记05-Convolution and Pooling Layers
tags: ["OMSCS", "CS7643-DL"]
key: OMSCS-DL-05
aside:
  toc: true
sidebar:
  nav: OMSCS-DL
---

> 这个系列是Gatech OMSCS 深度学习课程([CS 7643: Deep Learning](https://omscs.gatech.edu/cs-7643-deep-learning))的同步课程笔记。课程内容涉及深度学习的基本理论方法以及它在计算机视觉、自然语言处理以及决策理论等领域中的应用，本节主要介绍深度学习中的卷积层和池化层。
<!--more-->

## Convolution Layers

### Limitation of Linear Layers

在前面的课程中我们介绍过计算图和自动微分的概念。通过自动微分技术我们可以把任意可微的操作封装成一个计算图，并且利用反向传播来更新参数。这样整个模型的瓶颈就在于内存，只要模型能够放入到内存中我们就可以进行优化。

<div align=center>
<img src="https://i.imgur.com/55xEHM5.png" width="80%">
</div>

目前我们只介绍了线性层来对输入数据进行变换。对于输入为M维输出为N维的数据，线性层共需要M*N+N个参数。对于图像这种维度很高的数据而言线性层的参数是非常庞大的；更重要的是更多的模型参数意味着更高的模型复杂度，要训练这样巨大的模型需要有非常多的数据才能保证不出现过拟合的问题。

<div align=center>
<img src="https://i.imgur.com/jaXAR7F.png" width="80%">
</div>

### Locality of Features

实际上对于图像这种数据我们并不需要如此多的参数来建立模型。图像这类数据的特点是它具有局部性，换句话说图像上的特征都只与它附近的数据相关与远处的数据无关。

<div align=center>
<img src="https://i.imgur.com/T3T8Wej.png" width="80%">
</div>

#### Receptive Fields

由于特征是局部的，在提取特征时我们不用把全图都考虑进来而只需要考虑一个小窗口上的区域即可，这个区域称为**感受野(receptive field)**。根据感受野的假定，我们可以把提取每个特征的参数量从M * N + N降低到(K1 * K2 + 1) * N，这样就极大地降低了模型的复杂度。

<div align=center>
<img src="https://i.imgur.com/OYTGgq9.png" width="80%">
</div>

#### Shared Weights

在感受野的基础上我们可以进一步假定输出的节点上都对应相同的特征，也就是说计算每个特征的权重是共享的。这样，每个特征对应的参数就降低为K1 * K2 + 1。

<div align=center>
<img src="https://i.imgur.com/eBYik2j.png" width="80%">
</div>

#### Learn Many Features

在每个邻域上我们可以同时计算多个特征，这样可以提高模型的表达能力。此时整个计算特征的参数量为(K1 * K2 + 1) * M。

<div align=center>
<img src="https://i.imgur.com/x0qv0AP.png" width="80%">
</div>

### Convolution

实际上**卷积(convolution)**运算就是满足上面三条假定的运算。在信号处理和计算机视觉等领域中卷积运算有着大量的应用，我们可以通过卷积运算来得到输入信号在不同特征上的相应。

<div align=center>
<img src="https://i.imgur.com/IiSF4DZ.png" width="80%">
</div>

卷积运算的数学表达式如下。

<div align=center>
<img src="https://i.imgur.com/xltzvrN.png" width="80%">
<img src="https://i.imgur.com/xFETaNj.png" width="75%">
</div>

对于给定的卷积核K，卷积运算可以理解为首先将K旋转90°然后在图像上进行滑动，在滑动时提取图像对应区域进行相乘并求和。

<div align=center>
<img src="https://i.imgur.com/H2dX1E3.png" width="80%">
<img src="https://i.imgur.com/gTksPD2.png" width="80%">
<img src="https://i.imgur.com/DnvydbD.png" width="80%">
</div>

### Cross-Correlation

与卷积类似的图像变换是**相关(cross-correlation)**，它也需要将核K在图像上滑动并求和。但与卷积不同的是相关运算不需要先对K进行旋转，只需要直接让K进行滑动即可。

<div align=center>
<img src="https://i.imgur.com/AEGVorv.png" width="80%">
</div>

在实际进行编程时我们不会区分卷积核相关的概念，而是统一使用相关进行运算。这一方面是因为相关运算比较简单易于实现，更重要的是我们不会指定核而是通过学习的方式来获得核的值。从这样的角度上讲，使用相关来代替卷积更方便我们理解计算的过程。

<div align=center>
<img src="https://i.imgur.com/Un7DvJk.png" width="80%">
<img src="https://i.imgur.com/eCDYQ5q.png" width="80%">
</div>

## Input and Output Sizes

## Pooling Layers
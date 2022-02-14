---
layout: article
title: OMSCS-DL课程笔记07-Visualization
tags: ["OMSCS", "CS7643-DL"]
key: OMSCS-DL-07
aside:
  toc: true
sidebar:
  nav: OMSCS-DL
---

> 这个系列是Gatech OMSCS 深度学习课程([CS 7643: Deep Learning](https://omscs.gatech.edu/cs-7643-deep-learning))的同步课程笔记。课程内容涉及深度学习的基本理论方法以及它在计算机视觉、自然语言处理以及决策理论等领域中的应用，本节主要介绍深度学习中的可视化方法。
<!--more-->

## Visualization of Neural Networks

当我们训练好模型后可以通过一些可视化方法去理解网络在训练过程中到底学习到了什么内容。常用的可视化方法可以分为对模型权重(参数)的可视化、对输入数据响应的可视化、基于梯度的可视化以及对输入数据进行扰动来测试模型鲁棒性几种类型。

<div align=center>
<img src="https://i.imgur.com/CBswuv4.png" width="80%">
</div>

### Visualizing Weights

最基础的可视化方法是对网络的权重进行可视化。以全连接层为例，我们可以把全连接层的参数reshape成与输入图像一致的尺寸，然后将参数的范围规范化到[0, 255]区间上进行可视化。通过这种方法可以发现不同类别的分类器对应的权重都类似于相应类别的图片，这说明网络在训练过程中学习到了不同类别在图像上的表示。而对于卷积层，我们可以直接把每个卷积核的取值进行规范化，然后按照图像的格式进行显示。可视化的结果显示卷积核会对某些特定类型的图像特征有着强烈的响应。

<div align=center>
<img src="https://i.imgur.com/YffEij3.png" width="80%">
</div>

### Visualizing Output Maps

我们同样可以提取网络的一些中间层输出结果进行可视化。需要注意的是由于池化的存在深层输出的尺寸可能都比较小，因此这种方法只适用于一些浅层的输出。

<div align=center>
<img src="https://i.imgur.com/cv8kezw.png" width="80%">
</div>

可视化的结果显示不同的卷积核会对输入图像上的特定区域有着比较强的相应，而这些区域也往往对应着图像上的一些特定的内容(眼睛、面孔等)。

<div align=center>
<img src="https://i.imgur.com/bWasUgz.png" width="80%">
</div>

### Dimensionality Reduction

除此之外我们还可以使用一些降维的方法来可视化高维的输出数据。由于这些数据往往具有很强的非线性关系，一般会使用t-SNE这样的降维算法来进行可视化。可视化的结果显示具有相同类别的特征向量往往会出现在同一个聚类中。

<div align=center>
<img src="https://i.imgur.com/Pz5Ifua.png" width="80%">
</div>

上述这些可视化方法可以帮助我们理解神经网络学习到了什么内容，但有时这些可视化的结果可能是难以解释甚至是带有误导性质的。同时需要注意的是神经网络学习到的特征往往是分布式的，单个神经元可能无法完整的表达某个特征的全部内容，这就使得对神经网络进行解释更加困难。

<div align=center>
<img src="https://i.imgur.com/4xuzUdC.png" width="80%">
</div>

## Gradient-Based Visualizations

### Gradient of Loss w.r.t. Image

#### Object Segmentation for Free!

#### Detecting Bias

### Gradient of Activation w.r.t. Input

#### Guided Backprop

#### Grad-CAM

## Optimizing the Input Images

## Testing Robustness

## Style Transfer
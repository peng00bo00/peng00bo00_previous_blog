---
layout: article
title: OMSCS-DL课程笔记06-Convolutional Neural Network Architectures
tags: ["OMSCS", "CS7643-DL"]
key: OMSCS-DL-06
aside:
  toc: true
sidebar:
  nav: OMSCS-DL
---

> 这个系列是Gatech OMSCS 深度学习课程([CS 7643: Deep Learning](https://omscs.gatech.edu/cs-7643-deep-learning))的同步课程笔记。课程内容涉及深度学习的基本理论方法以及它在计算机视觉、自然语言处理以及决策理论等领域中的应用，本节主要介绍卷积神经网络的结构。
<!--more-->

## Backwards Pass for Convolution Layer

在上一节中我们介绍过卷积层的定义以及前向传播过程，而对于神经网络来说只知道前向传播是不够的，我们还需要了解卷积层的反向传播过程。首先我们来回忆一下卷积的前向传播，对于输出特征图上的每一点$y[r, c]$我们提取输入图像上的窗口$x[r:r+k_1, c:c+k_2]$然后和卷积核$k$进行内积计算作为卷积的输出值。

<div align=center>
<img src="https://i.imgur.com/fRnnb1T.png" width="80%">
<img src="https://i.imgur.com/jBa9PJK.png" width="80%">
</div>

因此对于输出特征图上的每一点$y[r, c]$它只包含线性运算。当我们已知损失函数对于输出层的导数$\frac{\partial L}{\partial y}$时，就可以利用线性运算的反向传播公式来计算损失函数$L$关于输入$x$和卷积核$k$的导数。

<div align=center>
<img src="https://i.imgur.com/z5GiIws.png" width="80%">
</div>

## Gradient for Convolution Layer

首先来考虑输出特征图关于卷积核的导数。由于特征图$y$上每一个像素都是使用同一个卷积核$k$进行计算得到，我们需要计算$y$上每个像素关于卷积核的导数$\frac{\partial y[r, c]}{\partial k}$并把它们加起来作为卷积核的导数。

<div align=center>
<img src="https://i.imgur.com/GNQbPZ8.png" width="80%">
</div>

具体来说，损失函数关于卷积核的导数$\frac{\partial L}{\partial k}$可通过上游的导数$\frac{\partial L}{\partial y[r, c]}$以及局部导数$\frac{\partial y[r, c]}{\partial k}$相乘来获得。由于卷积核$k$参与了$y$上所有像素值的计算，我们还需要再对$y$上的所有像素求和才能得到最终的导数。

<div align=center>
<img src="https://i.imgur.com/h4U5teW.png" width="80%">
</div>

由于卷积是线性变换，我们可以进一步把局部导数$\frac{\partial y[r, c]}{\partial k}$代换为输入图像对应位置的像素值。这样不难发现损失函数关于卷积核的导数等于上游导数与输入图像的卷积(相关)。

<div align=center>
<img src="https://i.imgur.com/1rZyHg1.png" width="80%">
<img src="https://i.imgur.com/oaQukpu.png" width="80%">
</div>

接下来考虑输出特征图关于输入特征图的导数。类似于计算卷积核导数的过程，我们同样需要对输出特征图上的导数进行求和，不过对于输入特征图上的像素$x[r, c]$我们只需要考虑它的邻域即可。

<div align=center>
<img src="https://i.imgur.com/yMyKyiL.png" width="80%">
<img src="https://i.imgur.com/mMCX5yO.png" width="80%">
<img src="https://i.imgur.com/8CvGAON.png" width="80%">
</div>

我们同样对求和公式进行变形，可以发现损失函数关于输入特征图的导数等于上游导数与卷积核的卷积。

<div align=center>
<img src="https://i.imgur.com/oDUnDp9.png" width="80%">
<img src="https://i.imgur.com/1lD7ApR.png" width="80%">
<img src="https://i.imgur.com/9pC4gvi.png" width="80%">
</div>

## Simple Convolutional Neural Networks

### Combining Convolution & Pooling Layers

我们把卷积层和池化层也加进神经网络中就得到了**卷积神经网络(convolutional neural networks, CNN)**。

<div align=center>
<img src="https://i.imgur.com/GiND15U.png" width="80%">
</div>

典型的CNN通常还包括**全连接层(fully connected layers)**作为最终的分类器，这样整个网络可以理解为将图像输入到卷积层中提取特征然后利用全连接层对提取到的特征进行分类。

<div align=center>
<img src="https://i.imgur.com/lYoi2bL.png" width="80%">
<img src="https://i.imgur.com/jR79SHy.png" width="80%">
</div>

CNN中一个常见的概念是**感受野(receptive fields)**。随着卷积层和池化层的增加特征图的长和宽尺寸会不但减少，因此特征图上每一个像素对应输入图像的区域会不断增加。这个对应的区域称为"感受野"。

<div align=center>
<img src="https://i.imgur.com/loGXuqV.png" width="80%">
</div>

### LeNet Architecture

这样的网络结构可以追溯到80年代的LeNet，当时研究人员就提出了这种结构的CNN来进行手写数字和字母的识别。

<div align=center>
<img src="https://i.imgur.com/35FaNIP.png" width="80%">
<img src="https://i.imgur.com/0LDcKkz.png" width="80%">
</div>

由于CNN具有平移不变性和一定程度的旋转不变性，LeNet对于输入图片的几何变换都有比较好的适应性。

<div align=center>
<img src="https://i.imgur.com/wjcIxuk.png" width="80%">
<img src="https://i.imgur.com/DZM8mWW.png" width="80%">
<img src="https://i.imgur.com/HR7RsBa.png" width="80%">
</div>

## Advanced Convolutional Networks

### AlexNet

现代CNN的流行始于2012年，当时AlexNet以巨大优势击败了传统人工特征+分类器的图像识别方法，从此基于CNN的模型成为了计算机视觉和图像识别领域的主流方法。

<div align=center>
<img src="https://i.imgur.com/z1TOh9E.png" width="80%">
</div>

整体来看AlexNet与LeNet在结构上的差异不大，但AlexNet使用了更加先进的激活函数以及一些现代的正则化方法，同时在大规模训练数据以及数据增强技术的加持下AlexNet超越了所有的传统图像识别方法。

<div align=center>
<img src="https://i.imgur.com/SdOhgEK.png" width="80%">
</div>

### VGG

在AlexNet基础上人们还提出了各种各样的网络结构，比较经典的是VGG网络。和AlexNet相比，VGG包含更多的层数也因此有着更好的性能。

<div align=center>
<img src="https://i.imgur.com/m8oIsPT.jpg" width="80%">
<img src="https://i.imgur.com/bX39yLd.png" width="80%">
<img src="https://i.imgur.com/JF62kPF.png" width="80%">
</div>

### Inception Architecture

同时人们还发现一味增加网络深度有时并不会提高模型的性能，因此在GoogLeNet中提出了inception module这样的单元来提取图像特征。inception module的核心是在一个层中包含多个不同尺寸的卷积核，这样就可以提取到同一输入下不同尺度上的特征并加以融合。

<div align=center>
<img src="https://i.imgur.com/jkZfh8i.png" width="80%">
<img src="https://i.imgur.com/EMlMxQR.png" width="80%">
</div>

### Residual Blocks and Skip Connections

为了解决训练深层网络十分困难的问题，人们提出了残差连接这样的结构形式。它的核心是在卷积后将输出特征图像与输入特征图像相加，这样使得输入特征总是可以得到来自输出特征的导数，从而避免了梯度消失的问题。

<div align=center>
<img src="https://i.imgur.com/MWcmN2l.png" width="80%">
</div>

### Evolving Architectures and AutoML

近年来还涌现了一些基于进化算法以及强化学习的自动化网络设计方法，一些研究指出这类自动化网络设计方法可以超越以往的人工设计网络。除了寻找性能更好的网络结构外，一些研究还试图在保证性能的基础上减少模型的复杂度从而得到更高效的网络结构形式。

<div align=center>
<img src="https://i.imgur.com/fudd8Na.png" width="80%">
<img src="https://i.imgur.com/jhFzIeM.png" width="80%">
</div>

## Transfer Learning & Generalization
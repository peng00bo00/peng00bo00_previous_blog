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

## Advanced Convolutional Networks

## Transfer Learning & Generalization
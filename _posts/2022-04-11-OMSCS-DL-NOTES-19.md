---
layout: article
title: OMSCS-DL课程笔记19-Generative Models
tags: ["OMSCS", "CS7643-DL"]
key: OMSCS-DL-19
aside:
  toc: true
sidebar:
  nav: OMSCS-DL
---

> 这个系列是Gatech OMSCS 深度学习课程([CS 7643: Deep Learning](https://omscs.gatech.edu/cs-7643-deep-learning))的同步课程笔记。课程内容涉及深度学习的基本理论方法以及它在计算机视觉、自然语言处理以及决策理论等领域中的应用，本节主要介绍生成式模型。
<!--more-->

## Introduction

**生成式模型(generative models)**是无监督学习的一种算法，它的目标是对生成数据的分布进行建模。在传统机器学习中最经典的生成式模型是**高斯混合模型(Gaussian mixture model, GMM)**，而在深度学习时代我们则可以利用深度神经网络对更加复杂的数据分布进行建模。

<div align=center>
<img src="https://i.imgur.com/HxzADa4.png" width="80%">
</div>

从数学上来看，**判别式模型(discriminative model)**的本质是计算给定样本的后验概率$P(y \vert x)$，我们熟悉的神经网络以及SVM等模型大多属于这一类型；而生成式模型则是最大化生成已有样本的概率，对于参数化的模型这等价于**极大似然估计(maximum likelihood estimation, MLE)**。此外，当我们获得了生成式模型后就可以从分布中进行采样从而生成更多的数据样本。

<div align=center>
<img src="https://i.imgur.com/P5v3Jyk.png" width="80%">
</div>

显然如何获得生成式模型是比较困难的任务，目前常用的生成式模型算法可以归纳如下：

<div align=center>
<img src="https://i.imgur.com/yWG7O0Z.png" width="80%">
</div>

## PixelRNN & PixelCNN

对于一张图片而言，我们可以把它的似然函数分解为每个像素似然函数的乘积。这样整个图片可以看做是一个大型的**贝叶斯网络(Bayesian network)**或是**语言模型(language model)**，我们只需要定义像素之间的连接关系再估计似然函数的形式即可计算概率分布。

<div align=center>
<img src="https://i.imgur.com/VoZKG81.png" width="80%">
</div>

PixelRNN就是基于上述思想实现的生成式模型。在PixelRNN中我们需要设置像素之间的连接(生成)关系，然后从某一个像素出发利用RNN来计算下一个像素的概率。显然PixelRNN的计算效率是比较低的，并且在训练时我们无法使用整张图片而是只能通过预测少量的像素来进行训练。

<div align=center>
<img src="https://i.imgur.com/QsUX6Ig.png" width="80%">
</div>

PixelCNN的思想与PixelRNN类似，不过它使用了卷积核来代替RNN生成像素。和PixelRNN相比PixelCNN的训练过程要快很多，但在进行生成时仍然效率很低。

<div align=center>
<img src="https://i.imgur.com/xB6nGGP.png" width="80%">
</div>

PixelRNN和PixelCNN有很多有趣的应用，除了直接生成图片外我们还可以遮住图片中的一部分区域然后估计这片区域可能的形式。当然PixelRNN和PixelCNN的生成过程是不符合天然图片的生成过程的，这导致了它们生成出的图片在很多细节上有不正确的结果。

<div align=center>
<img src="https://i.imgur.com/Nw0NU5s.png" width="80%">
<img src="https://i.imgur.com/osR4OwU.png" width="80%">
</div>

## Generative Adversarial Networks

## Variational Autoencoders
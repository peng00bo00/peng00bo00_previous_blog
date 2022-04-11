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

**生成对抗网络(generative adversarial networks, GAN)**是最近几年比较流行的生成式模型。和传统方法相比，GAN是一种**隐式方法(implicit method)**：它不会直接去计算$P(x)$的形式而是去对$P(x)$的采样过程进行建模。

<div align=center>
<img src="https://i.imgur.com/arMFklG.png" width="80%">
</div>

GAN的本质是计算一个简单的分布(如标准正态分布$N(0, 1)$)到样本生成分布$P(x)$的映射，这样我们可以简单地从已知分布中进行采样然后利用一个神经网络将这个样本映射到所需数据分布上，就实现了从$P(x)$中进行采样的过程。

<div align=center>
<img src="https://i.imgur.com/bhaMnjB.png" width="80%">
<img src="https://i.imgur.com/5CD6EIG.png" width="80%">
</div>

当然要计算这样的一个分布到分布的映射没有那么的容易。在GAN中通过训练两个网络：**生成器(generator)**和**判别器(discriminator)**来实现完整的训练过程。其中生成器用来对样本进行映射，而判别器则用来判断生成器生成的样本是否足够接近真实的数据。

<div align=center>
<img src="https://i.imgur.com/fjWQ11x.png" width="80%">
<img src="https://i.imgur.com/XgQKqzo.png" width="80%">
</div>

### Mini-Max Two Player Game

GAN的训练过程可以视为两个网络相互博弈的过程。不过由于我们使用了神经网络来表示映射，目前尚不清楚这样的博弈过程是否能够达到**纳什均衡(Nash equilibria)**。对于生成器，它的优化目标是尽可能去让判别器相信它生成的样本是真实的数据；而判别器则是对真实样本和生成器的样本进行一个二分类，我们把真实的数据标记为正例而来自生成器的样本标记为反例。这样整个GAN的训练目标等价于求解一个极小极大问题：生成器负责极大化二分类损失，而判别器则是极小化损失。

<div align=center>
<img src="https://i.imgur.com/qjr2sku.png" width="80%">
<img src="https://i.imgur.com/G7OLA4K.png" width="80%">
<img src="https://i.imgur.com/BvjEGPY.png" width="80%">
<img src="https://i.imgur.com/CjVCTeP.png" width="80%">
</div>

以图像生成为例，GAN的训练过程如下：我们首先采样出一系列随机种子然后利用生成器产生一系列样本，然后从数据集中采样出等量的真实图片并把它们混合到一起送入判别器中进行二分类。由于整个过程都是可导的，我们可以利用标准的梯度下降方法来训练两个网络。

<div align=center>
<img src="https://i.imgur.com/uUNa394.png" width="80%">
</div>

在实践中人们还发现训练开始时生成器的样本与真实样本差距过大，导致生成器很难从判别器那里获得梯度。为了缓解这样的问题还可以稍微修正一下生成器的损失函数，这样可以提高GAN训练时的稳定性。

<div align=center>
<img src="https://i.imgur.com/7DrVZjP.png" width="80%">
</div>

完整的GAN训练流程则如下图所示：

<div align=center>
<img src="https://i.imgur.com/4UirbLW.png" width="80%">
</div>

当我们完成训练后就可以利用随机种子和生成器来生成逼真的数据样本，同时判别器中的一些特征可以服务于不同的分类任务。

<div align=center>
<img src="https://i.imgur.com/5nNN1kU.png" width="80%">
<img src="https://i.imgur.com/AP01Mgd.png" width="80%">
</div>

### Challenges

目前来看训练GAN仍然是相对困难的，因此人们提出了不同的方法来改进原始的GAN训练过程。这些方法包括使用更稳定的网络架构、为目标函数添加正则项以及使用渐进的训练方法等。

<div align=center>
<img src="https://i.imgur.com/nfgXPO8.png" width="80%">
</div>

DCGAN对GAN的网络模型进行修正，从而获得更稳定的训练过程。

<div align=center>
<img src="https://i.imgur.com/yqKdvpz.png" width="80%">
</div>

通过对GAN目标函数的理论分析，人们还提出了添加噪声作为正则项的改进方法。

<div align=center>
<img src="https://i.imgur.com/czHCHKN.png" width="80%">
</div>

基于这些改进，目前GAN相关的方法以及可以生成高分辨率的逼真图像，同时GAN也可以用来生成语音、视频等其它形式的数据。

<div align=center>
<img src="https://i.imgur.com/gmx7udH.png" width="80%">
<img src="https://i.imgur.com/xQkij75.png" width="80%">
<img src="https://i.imgur.com/1hgHWpN.png" width="80%">
</div>


<div align=center>
<img src="https://i.imgur.com/AUthuzy.png" width="80%">
</div>

## Variational Autoencoders
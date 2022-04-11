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

显然如何获得生成式模型是比较困难的任务，目前常用的生成式模型算法可以分类如下：

<div align=center>
<img src="https://i.imgur.com/yWG7O0Z.png" width="80%">
</div>

## PixelRNN & PixelCNN

## Variational Autoencoders
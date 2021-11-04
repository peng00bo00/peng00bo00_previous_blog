---
layout: article
title: OMSCS-CV课程笔记12-Generative Models
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-12
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍图像识别和生成式模型的相关内容。
<!--more-->

## Image Recognition

**图像识别(image recognition)**是计算机视觉中较为复杂的任务，我们希望计算机可以告诉我们图像中包含了哪些物体，它们的位置都在哪里，图像的场景是什么等问题。

<div align=center>
<img src="https://i.imgur.com/kG5Hgah.png" width="40%">
<img src="https://i.imgur.com/kG5Hgah.png" width="40%">
</div>

图像识别的难点很多，比如说现实中的图像往往容易收到光照因素的影响，同样的物体可能会有不同的姿态，图像中可能存在很多杂乱的物体对视线进行干扰等。

<div align=center>
<img src="https://i.imgur.com/5mJinzS.png" width="90%">
</div>

同时，现实中的图像或多或少会有一些遮挡的问题；同一类别的物体往往只存在细微的差别，这又提高了图像识别的难度；此外当相机的视角不同时同一个物体会有不同的呈现形式。这些都使得设计鲁棒的图像识别算法变得非常困难。

<div align=center>
<img src="https://i.imgur.com/5wGYzsT.png" width="90%">
</div>

不过近几年随着机器学习尤其是深度学习方法的流行，图像识别这一问题在很大程度上已经得到了解决。基于大数据和深度神经网络的图像识别方法在识别精度和正确率上已经接近或超越了人类水平，并在各个领域中都得到了大量的应用。

<div align=center>
<img src="https://i.imgur.com/xynzIgY.png" width="50%">
<img src="https://i.imgur.com/D3UBZqb.png" width="30%">
</div>

## Classification: Generative Models

在本课程中我们不会过多地讨论这些机器学习或深度学习方法，而是着重介绍使用机器学习解决图像识别的基本思想。以数字图像分类问题为例，给定一系列带有标签的训练图像，我们希望能从数据中学习到一个模型来识别图像中的数字：

<div align=center>
<img src="https://i.imgur.com/VuMhtYV.png" width="60%">
</div>

那么如何衡量这个模型的好坏呢？我们需要知道这个模型会犯哪些错误，以及当模型犯错时相应的损失是多少。显然我们希望模型在训练数据上的(期望)损失越小越好，这就是**监督学习(supervised learning)**的基本思想。一般来说监督学习方法有两种策略：

- 使用训练数据对不同类别的数据生成过程进行建模，分别计算不同类别的先验和条件概率，这样的方法称为**生成式模型(generative model)**；
- 直接学习不同类别数据的决策边界并对后验概率进行建模，这类方法称为**判别式模型(discriminative model)**。

这节课我们主要会关注生成式模型。回到数字图像分类的问题，我们可以定义模型$s$的**风险(risk)**为：

$$
R(s) = P(4 \rightarrow 9 \vert s) L(4 \rightarrow 9) + P(9 \rightarrow 4 \vert s) L(9 \rightarrow 4)
$$

其中$P(4 \rightarrow 9 \vert s)$和$P(9 \rightarrow 4 \vert s)$分别表示模型$s$发生错误的概率，$L(4 \rightarrow 9)$和$L(9 \rightarrow 4)$则是发生这种错误时产生的损失。

## Principle Component Analysis

## Appearance-Based Tracking
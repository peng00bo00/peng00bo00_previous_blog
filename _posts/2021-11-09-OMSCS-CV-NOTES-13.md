---
layout: article
title: OMSCS-CV课程笔记13-Discriminative Models
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-13
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍判别式模型的相关内容。
<!--more-->

## Classification: Discriminative Models

在上一节中我们介绍了分类问题中的生成式模型，它通过计算类别的先验以及似然来估计样本的类别。生成式模型有非常好的理论保证，但如何去表示高维数据的概率密度是十分困难的。同时在很多情况下我们并不关心数据的产生过程，只要有一个好的决策模型就可以满足我们的要求。因此在现代机器学习和计算机视觉中更加常用的是对决策边界进行建模的**判别式模型(discriminative model)**。

要使用判别式模型我们需要对数据进行如下假设：

- 每个样本所属的可能类别是确定的；
- 每个类别都拥有足够多的数据样本；
- 分类器可能犯的错误都具有相同的代价；
- 我们使用特征来表示每个样本，但我们事先并不知道哪些特征对于分类问题是更有效的。

在这样的假设下我们可以把求解图像识别的问题划分为训练和测试两个阶段：

- 在训练阶段中我们需要设计合适的特征来表示样本，并利用这些特征来训练分类器；
- 在测试阶段中我们需要将输入图像分解成若干的候选图像(candidate)，然后对这些图像进行打分来实现图像识别。

### Window-Based Models

在图像识别任务中常用的图像特征包括边缘、轮廓、图像梯度等，在构造图像特征时往往会将图像划分成网格然后在每个格子内计算这些特征的直方图作为最终的图像特征。

<div align=center>
<img src="https://i.imgur.com/yYwRoKH.png" width="80%">
</div>

以车辆检测为例，我们需要使用这些图像特征训练一个二元分类器来回答输入图像是否是一辆汽车。

<div align=center>
<img src="https://i.imgur.com/sh7SbyV.png" width="80%">
<img src="https://i.imgur.com/yqyBkUo.png" width="80%">
</div>

当模型训练好后，我们就可以在图像上进行滑窗来检测出图像中车汽车的位置。

<div align=center>
<img src="https://i.imgur.com/8gI2u1z.png" width="80%">
</div>

在计算机视觉中常用的分类模型如下：

<div align=center>
<img src="https://i.imgur.com/z0s2Y9O.png" width="80%">
</div>

## Boosting and Face Detection

## Support Vector Machines

## Bag of Visual Words

## Reference
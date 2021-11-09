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

### Boosting: Intuition

Boosting是一种常用的集成学习模型，它的基本思想是将一系列**弱学习器(weak learner)**组合到一起形成一个强大的模型。在训练过程中，boosting会提高当前学习器分类错误的样本权重从而在下一轮训练中更加关注这些错误的样本：

<div align=center>
<img src="https://i.imgur.com/lmUv2Ry.png" width="40%">
<img src="https://i.imgur.com/SofYVOc.png" width="40%">
</div>

<div align=center>
<img src="https://i.imgur.com/xrfsjLp.png" width="40%">
<img src="https://i.imgur.com/j158nFe.png" width="40%">
</div>

<div align=center>
<img src="https://i.imgur.com/JJViXfo.png" width="40%">
</div>

当训练完成时，最终的模型即为全部弱学习器的线性组合。每个学习器的权重则取决于所使用的boosting算法，如Adaboost中会根据分类器的错误率来调节弱学习器的权重，错误率越低则权重越大。

<div align=center>
<img src="https://i.imgur.com/UdSjdAl.png" width="60%">
</div>

### Viola-Jones Face Detector

Boosting在计算机视觉中的经典应用是Viola-Jones人脸检测算法，它的基本思想是使用一系列方块形滤波器构造出人脸的特征并训练出一个二分类模型进行人脸检测。

<div align=center>
<img src="https://i.imgur.com/uZtQgJ1.png" width="80%">
</div>

在原始论文中检测窗口固定为$24 \times 24$，根据滤波器的位置、尺寸和形状总共有超过180,000种可能的特征(滤波器)。

<div align=center>
<img src="https://i.imgur.com/6AhjIQq.png" width="60%">
</div>

然后使用Adaboost算法来训练人脸分类器，其中每个弱学习器只在几个少量的特征上进行分类，即每个学习器都只选择当前最有效的特征进行学习。

<div align=center>
<img src="https://i.imgur.com/TFYT6FB.png" width="60%">
</div>

同时在实践中还发现图像中大部分位置都不是人脸，因此为了提高效率Viola-Jones人脸检测算法还设计了一个**级联分类器(cascade classifier)**来过滤掉图像中非人脸的部分。它的思想是将一系列分类器串联起来，当输入窗口图像被当前分类器划分为负样本时直接拒绝它，换句话说只有通过所有分类器的窗口才是人脸。

<div align=center>
<img src="https://i.imgur.com/ZSj1WK3.png" width="60%">
</div>

Viola-Jones人脸检测算法的基本框架如下：

<div align=center>
<img src="https://i.imgur.com/zEzL6s8.png" width="80%">
</div>

Viola-Jones人脸检测算法是第一个大规模应用的人脸检测算法，一些检测结果如下：

<div align=center>
<img src="https://i.imgur.com/awv2J1G.png" width="80%">
</div>

## Support Vector Machines

## Bag of Visual Words

## Reference

- [Wikipedia: AdaBoost](https://en.wikipedia.org/wiki/AdaBoost)
- [Wikipedia: Viola–Jones object detection framework](https://en.wikipedia.org/wiki/Viola%E2%80%93Jones_object_detection_framework)
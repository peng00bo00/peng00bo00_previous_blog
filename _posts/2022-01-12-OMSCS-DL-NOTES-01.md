---
layout: article
title: OMSCS-DL课程笔记01-Linear Classifiers and Gradient Descent
tags: ["OMSCS", "CS7643-DL"]
key: OMSCS-DL-01
aside:
  toc: true
sidebar:
  nav: OMSCS-DL
---

> 这个系列是Gatech OMSCS 深度学习课程([CS 7643: Deep Learning](https://omscs.gatech.edu/cs-7643-deep-learning))的同步课程笔记。课程内容涉及深度学习的基本理论方法以及它在计算机视觉、自然语言处理以及决策理论等领域中的应用，本节主要回顾线性分类器以及梯度下降法在机器学习中的应用。
<!--more-->

## Machine Learning Overview

**机器学习(machine learning, ML)**是目前整个计算机科学中最为火热的研究领域之一。和传统的算法研究相比，机器学习的特点是算法会在和数据进行交互的过程中不断提升自身的性能。

<div align=center>
<img src="https://i.imgur.com/JQjtSas.png" width="80%">
</div>

同时，对于很多问题我们可能很难直接设计算法进行求解，有时甚至很难去精确地定义问题。在这种情况下，我们就可以利用机器学习这种数据驱动的方式来进行求解。

<div align=center>
<img src="https://i.imgur.com/4OAttGo.png" width="80%">
</div>

从研究领域来划分，机器学习属于广义**人工智能(artificial intelligence, AI)**的一个子集，而**深度学习(deep learning)**则是机器学习的一个子集。

<div align=center>
<img src="https://i.imgur.com/5sWRDGQ.png" width="80%">
</div>

目前，基于深度学习的机器学习技术已经成为整个学术界研究的主流方法。同时深度学习在计算机视觉**(computer vision, CV)**、**自然语言处理(natural language processing, NLP)**、**决策科学(decision making)**、**机器人系统(robotics)**等诸多领域中都取得了大量的应用。

<div align=center>
<img src="https://i.imgur.com/C19nbnN.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/Et3Fcll.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/KWiO8WR.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/IBQ1nB9.png" width="80%">
</div>

## Supervised Learning and Parametric Models

根据提供数据的类型，机器学习大体可以分为**监督学习(supervised learning)**、**无监督学习(unsupervised Learning)**以及**强化学习(reinforcement Learning)**三种。

<div align=center>
<img src="https://i.imgur.com/Jtjcx6p.png" width="80%">
</div>

其中监督学习是指对于给定的数据$X$和标签$Y$，算法通过不断的学习输出一个函数$f$将$X$映射为$Y$。基于深度学习的监督学习算法已经取得了非常显著的效果，在本课程中也主要介绍深度学习在监督学习范畴中的应用。

<div align=center>
<img src="https://i.imgur.com/4NEaFSM.png" width="80%">
</div>

### Supervised Learning

根据模型是否具有参数，监督学习还可以细分为参数化模型和非参数化模型两类。前者的代表是**逻辑回归(logistic regression)**和**神经网络(neural networks)**，而后者的代表则包括**决策树(decision tree)**和**kNN(k nearest neighbor)**。

<div align=center>
<img src="https://i.imgur.com/teS9jEN.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/4qntRan.png" width="80%">
</div>

### Traditional Machine Learning

以图像分类为例，在深度学习诞生之前的经典分类算法是利用一个参数模型$f(x, W)$将输入图像映射为一个类别向量，然后去得分最高的那个维度作为图像的分类结果。

<div align=center>
<img src="https://i.imgur.com/QRV908Q.png" width="80%">
</div>

由于图像是一个高维的数组，直接带入模型进行训练的效率非常低，因此往往会利用人工设计的图像特征(如直方图)来表示整张图像。这样整个计算流程可以划分为特征工程和分类模型两部分。

<div align=center>
<img src="https://i.imgur.com/O359SH1.png" width="80%">
</div>

## Components of Parametric Learning

## Gradient Descent

## How is Deep Learning Different?
---
layout: article
title: OMSCS-DL课程笔记09-Advanced Computer Vision Architectures
tags: ["OMSCS", "CS7643-DL"]
key: OMSCS-DL-09
aside:
  toc: true
sidebar:
  nav: OMSCS-DL
---

> 这个系列是Gatech OMSCS 深度学习课程([CS 7643: Deep Learning](https://omscs.gatech.edu/cs-7643-deep-learning))的同步课程笔记。课程内容涉及深度学习的基本理论方法以及它在计算机视觉、自然语言处理以及决策理论等领域中的应用，本节主要介绍深度学习在图像分割以及目标检测中的应用。
<!--more-->

除了前面介绍过的图像分类，深度学习在很多更高级的计算机视觉任务中也有着大量的应用。

<div align=center>
<img src="https://i.imgur.com/82iqo1Y.png" width="80%">
</div>

## Image Segmentation Networks

### Segmentation Tasks

**图像分割(image segmentation)**是计算机视觉中的高级视觉任务，对于给定点输入图片我们希望获得它每个像素对应的标签。而图像分类还可以细分为**语义分割(semantic segmentation)**和**实例分割(instance segmentation)**两类，语义分割只需要获得像素的类别标签而实例分割还需要获得每个像素的物体编号。

<div align=center>
<img src="https://i.imgur.com/yYn9svy.png" width="80%">
</div>

显然对于图像分割任务我们的输出不再是一个类别编号，而是一张包含每个像素类别的特征图。因此对于图像分割网络我们需要一些额外的处理方式来获得类别特征图。

<div align=center>
<img src="https://i.imgur.com/ZJRS8zG.png" width="80%">
</div>

### Fully-Convolutional Network

**FCN(Fully-Convolutional Network)**是最早使用深度学习来解决图像分割任务的模型。它的基本思想是使用卷积层来替换掉分类网络最后的全连接层，同时最后一个卷积层的输出对应每个像素在不同类别上的概率。由于卷积层仍然是进行了线性运算，替换后的效果和全连接层是类似的，但此时我们则可以获得每个像素对应的类别。

<div align=center>
<img src="https://i.imgur.com/3sJetcj.png" width="80%">
<img src="https://i.imgur.com/whFObXs.png" width="80%">
</div>

卷积层的特点是参数量与输入的尺寸无关，因此FCN可以适应任意尺寸的图像作为输入。当输入图像的分辨率比较高时，通过FCN可以直接获得每个像素在不同类别上的概率(热力图)。

<div align=center>
<img src="https://i.imgur.com/8PQrS7N.png" width="80%">
<img src="https://i.imgur.com/MZv0mNK.png" width="80%">
</div>

### DeConvolution and UnPooling

FCN的缺陷在于输入图像经过网络后分辨率会缩减，造成一部分信息的损失。而对于现代的图像分割网络则一般会通过一些**反卷积(deconvolution)**和**反池化(unpooling)**的方式来恢复原始分辨率。

<div align=center>
<img src="https://i.imgur.com/FaXiu8B.png" width="80%">
</div>

#### UnPooling

反池化的运算类似于池化在反向传播中的计算流程。首先需要记录下池化时最大元素的位置，然后在反池化中将元素填入到对应位置从而恢复池化后的分辨率。

<div align=center>
<img src="https://i.imgur.com/1PlxbJB.png" width="80%">
<img src="https://i.imgur.com/M2NIMDp.png" width="80%">
<img src="https://i.imgur.com/ZtWkUjU.png" width="80%">
</div>

因此反池化要求将网络对称布置，形成**编码器-解码器(encoder-decoder)**的结构形式。

<div align=center>
<img src="https://i.imgur.com/wFgfzKJ.png" width="80%">
</div>

#### Transposed Convolution

类似于池化和反池化的关系，卷积运算的逆运算称为反卷积或**转置卷积(transposed convolution)**。在转置卷积运算中需要把卷积核乘以输入图像每个位置上的值，然后放置到输出图像的对应位置上。

<div align=center>
<img src="https://i.imgur.com/lEr5JL2.png" width="80%">
<img src="https://i.imgur.com/Vyo9Zlb.png" width="80%">
</div>

我们同样把转置卷积和卷积对称布置，这样整个网络输出的尺寸就和输入图像一致了。

<div align=center>
<img src="https://i.imgur.com/xHu0xsW.png" width="80%">
</div>

### Transfer Learning

从网络结构的角度上看，encoder部分的网络与一般的图像分类网络没有任何差异。因此我们可以使用迁移学习的方式用分类网络进行预训练，从而提高图像分割的准确率。

<div align=center>
<img src="https://i.imgur.com/VSeElHI.png" width="80%">
</div>

除此之外我们也可以借鉴分类网络的设计思想，把skip connection这样的结构应用在图像分割网络中来提高模型的性能。

<div align=center>
<img src="https://i.imgur.com/y0v9Nij.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/MTXmwYI.png" width="80%">
</div>

## Single-Stage Object Detection

## Two-Stage Object Detectors

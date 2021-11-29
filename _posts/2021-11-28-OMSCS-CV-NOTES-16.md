---
layout: article
title: OMSCS-CV课程笔记16-Binary Morphology
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-16
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍数学形态学的相关内容。
<!--more-->

## Binary Image Analysis

**二值图像(binary image)**是指仅包含0和1的图像。二值图像虽然简单但在计算机视觉中有着广泛的应用，我们可以使用0来表示背景并且用1来表示前景，这样就可以表示图像中的物体。除此之外，我们还可以对不相连的前景进行计数来获得图像中物体的数量、大小等信息。

<div align=center>
<img src="https://i.imgur.com/DZVDBXI.png" width="40%">
</div>

### Thresholding

获得二值图像最简单的方法是对灰度图像进行**阈值化(thresholding)**。所谓"阈值化"是指选择一个阈值将图像划分为前景和背景两部分，通常情况下小于阈值的部分划分背景(0)而大于阈值的为前景(1)。以下图为例，我们希望从图像中提取到水果的区域，首先需要统计图像的灰度直方图然后选择一个合适的灰度值进行阈值化：

<div align=center>
<img src="https://i.imgur.com/qeQiLV9.png" width="70%">
</div>

那么如何选择合适的阈值呢？一个直观的想法是遍历所有可能的灰度取值，然后选择其中最好的那个作为阈值。我们假设灰度直方图有两个峰值，然后对每个阈值$t$计算阈值化后前景和背景的灰度方差，选择方差之和最小的作为最终的分割阈值。这种算法称为**大津算法(Otsu's method)**，在二值图像分割中有着重要的应用。

<div align=center>
<img src="https://i.imgur.com/FQ25P46.png" width="40%">
</div>

### Connected Components Labeling

在很多情况下我们希望能够获得二值图像中互不相连的前景物体，这个过程称为**连通分量标记(connected-component labeling)**。求解连通分量标记的经典方法是进行两次扫描：首先逐行进行扫描，每当遇到同一行上互不相连的前景就令标记编号加1，如果当前位置的邻域已经标记过就选择邻域最小的编号：

<div align=center>
<img src="https://i.imgur.com/TSwI7Yo.png" width="70%">
</div>

然后进行第二次扫描，每当发现当前位置上方的标记大于自身时需要重新对上面的标记赋值，同时以它为起点将新的标记传播上去：

<div align=center>
<img src="https://i.imgur.com/vX46pYs.png" width="70%">
</div>

重新标记后就图像中互不连通的物体就获得了相应的标记：

<div align=center>
<img src="https://i.imgur.com/s32q2oU.png" width="70%">
</div>

连通分量标记在现实生活中有着非常多的应用，比如说在医学影像中来标记人体的不同器官，或是将标记映射为不同的颜色来实现一些图像效果：

<div align=center>
<img src="https://i.imgur.com/pE8hyYi.png" width="70%">
</div>

<div align=center>
<img src="https://i.imgur.com/7iZnird.png" width="70%">
</div>

## Mathematical Morphology

### Dilation and Erosion

### Opening and Closing

### Basic Morphological Algorithms

## Reference

- [Wikipedia: Otsu's method](https://en.wikipedia.org/wiki/Otsu%27s_method)
- [Wikipedia: Connected-component labeling](https://en.wikipedia.org/wiki/Connected-component_labeling)
- [Wikipedia: Mathematical morphology](https://en.wikipedia.org/wiki/Mathematical_morphology)
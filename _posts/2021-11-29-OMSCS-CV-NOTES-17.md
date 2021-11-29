---
layout: article
title: OMSCS-CV课程笔记17-3D Perception
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-17
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍三维感知的相关内容。
<!--more-->

## Motivation

在本门课程中我们介绍了对二维图像进行处理的各种算法，然而单张图像可能无法很好地表示三维空间中的物体。实际上图像有着很多的缺陷，比如说同样的物体在不同的光照条件下会有不同的颜色(color inconsistency)、无法通过图像恢复物体的绝对尺度、当物体本身缺乏纹理或是与背景比较相似时难以对其进行区分等等。

<div align=center>
<img src="https://i.imgur.com/FBrl35S.png" width="50%">
</div>

<div align=center>
<img src="https://i.imgur.com/gwdRSKE.png" width="30%">
<img src="https://i.imgur.com/hWy6vMR.png" width="31%">
<img src="https://i.imgur.com/rs0YtNI.png" width="28%">
</div>

因此我们希望能够更好地表达三维世界中的物体，这样的过程称为**三维感知(3D sensing)**。

<div align=center>
<img src="https://i.imgur.com/CLXHwJY.png" width="50%">
</div>

## 3D Sensing

根据成像的原理3D sensing可以分为被动和主动两种。

### Passive 3D sensing

被动感知一般是指利用自然环境中的光源和一些几何或是场景中的信息来实现三维物体的感知。被动感知的基本方法是使用双目相机来重建物体的深度，而在电影工业中有时还会使用更多的相机来提高重建的精度。

<div align=center>
<img src="https://i.imgur.com/e4DwbRS.png" width="70%">
</div>

除此之外还有一些研究表明我们可以利用焦距信息来重建物体的深度。

<div align=center>
<img src="https://i.imgur.com/j6RCzp3.png" width="40%">
</div>

### Active 3D sensing

主动感知则一般是指通过一些人工的光源以及物体在光源下的反应来实现对物体的感知。前面课程介绍过的[光度立体](/2021/10/05/OMSCS-CV-NOTES-09.html#shape-from-shading)就是一种主动感知方法，我们可以利用不同方向光线下的图像来重建物体的表面：

<div align=center>
<img src="https://i.imgur.com/xsYyPyJ.png" width="70%">
</div>

像激光雷达和声呐则使用了**飞行时间(time of flight, ToF)**来测量物体到传感器的距离：

<div align=center>
<img src="https://i.imgur.com/7UYbi7W.png" width="30%">
<img src="https://i.imgur.com/WZNM9VX.png" width="30%">
</div>

我们还可以使用**结构光(structured light)**来进行重建。结构光和双目相机非常相似，但不同的是结构光使用了投影仪来代替一个相机，并且投影仪会发出条纹状的光线从而在物体表面形成纹理。这样在重建时就可以利用条纹的先验信息以及它在物体上的响应来重建表面。

<div align=center>
<img src="https://i.imgur.com/1NaJ9vh.png" width="40%">
</div>

在Kinect中则使用了类似于结构光的技术。不过Kinect使用了红外光来发射信号，此时信号的发射和接收端都是Kinect自身。而且接收到的图案与物体的距离有关，因此可以利用图案的变化来反推出距离。和可见光相比，使用红外的优势在于它能够处理弱光环境下的成像问题，而且不依赖于物体自身或是环境的纹理。但需要注意的是红外光成像一般不能用于室外环境，而且图像分辨率会相对低一些。

<div align=center>
<img src="https://i.imgur.com/wDRYGxa.png" width="40%">
</div>

## Representation

### Depth Images

### Point Clouds
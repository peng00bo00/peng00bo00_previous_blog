---
layout: article
title: OMSCS-CV课程笔记07-Multiple Views
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-07
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍多视图几何的相关内容。
<!--more-->

## Image to Image Projections

在正式介绍多视图几何的相关内容前我们首先来考虑一下平面上的几何变换。平面上的几何变换可以分为**平移变换(translation)**、**刚体(欧式)变换(Euclidean transform)**、**相似变换(similarity transform)**以及**仿射变换(affine transform)**，而它们都可以看做是**投影变换(projective transform)**的特例。

<div align=center>
<img src="https://i.imgur.com/qV6Uush.png" width="70%">
</div>

通过齐次坐标可以把这些变换写成通用的形式：

$$
\begin{bmatrix}
x' \\ y' \\ w'
\end{bmatrix}
=
\begin{bmatrix}
a & b & c \\ d & e & f \\ g & h & i
\end{bmatrix}
\begin{bmatrix}
x \\ y \\ w
\end{bmatrix}
$$

$$
x' = H x
$$

其中矩阵$H$称为**单应矩阵(homography)**，它刻画了平面到平面的坐标变换关系。

### Translation

最基本的平面变换是平移变换，它的单应矩阵形式为：

$$
H = 
\begin{bmatrix}
1 & 0 & t_x \\ 0 & 1 & t_y \\ 0 & 0 & 1
\end{bmatrix}
$$

<div align=center>
<img src="https://i.imgur.com/n4j0rTX.png" width="50%">
</div>

显然在平移变换前后物体的夹角、长度、面积、朝向等几何量都保持不变。

### Euclidean Transform

在平移变换的基础上加入旋转就得到了刚体变换，对应的单应矩阵形式为：

$$
H = 
\begin{bmatrix}
\cos{\theta} & -\sin{\theta} & t_x \\ \sin{\theta} & \cos{\theta} & t_y \\ 0 & 0 & 1
\end{bmatrix}
$$

<div align=center>
<img src="https://i.imgur.com/QpEdkMr.png" width="50%">
</div>

显然物体的朝向在变换后会发生改变，但夹角、长度、面积保持不变。

### Similarity Transform

如果允许对平移变换后的物体进行缩放就得到了相似变换，它的单应矩阵为：

$$
H = 
\begin{bmatrix}
a \cos{\theta} & -a \sin{\theta} & t_x \\ a \sin{\theta} & a \cos{\theta} & t_y \\ 0 & 0 & 1
\end{bmatrix}
$$

<div align=center>
<img src="https://i.imgur.com/OGWX6Pz.png" width="50%">
</div>

相似变换后的物体只能保证夹角大小不变，物体的面积和长度则会按照相似比例变化。

### Affine Transform

进一步放宽约束条件可以得到仿射变换：

$$
H = 
\begin{bmatrix}
a & b & c \\ d & e & f \\ 0 & 0 & 1
\end{bmatrix}
$$

<div align=center>
<img src="https://i.imgur.com/4407cCM.png" width="50%">
</div>

仿射变换可以保证平行的直线经过变换后仍然保持平行。

### Projective Transform

最后，利用齐次坐标的归一化性质可以投影变换的但应矩阵：

$$
H = 
\begin{bmatrix}
a & b & c \\ d & e & f \\ g & h & 1
\end{bmatrix}
$$

<div align=center>
<img src="https://i.imgur.com/kb4S2bs.png" width="50%">
</div>

投影变换只能保证直线在变换后仍保持直线，但不能保证平行的直线变换后保持平行。

我们把前面介绍的这几种变换的性质进行汇总，可以得到如下的表格：

<div align=center>
<img src="https://i.imgur.com/mIT1Ue6.png" width="60%">
</div>

## Homographies and Mosaics

图像上的齐次坐标实际上可以从三维空间进行理解。此时多出来的一维$w$表示空间点的深度，因此图像平面上的点实际上表示的是空间中位于平面$z=1$上的点。同时利用齐次坐标的规范化性质，坐标$(x, y, 1)$可以理解为从原点出发经过图像平面上点$(x, y, 1)$的射线。

<div align=center>
<img src="https://i.imgur.com/Q56tdOx.png" width="30%">
</div>

利用齐次坐标的几何意义可以实现图像平面到图像平面的变换。假设空间中存在2个具有相同成像中心的图像平面PP1和PP2，我们想要计算两个图像平面的变换关系。对于空间中的点P可以做一条成像中心C到P点的连线与图像平面分别交于P1和P2两点，如下图所示：

<div align=center>
<img src="https://i.imgur.com/eMIOhuM.png" width="30%">
</div>

不难发现实际上我们不需要考虑两个平面的空间关系，只需要知道投影点的坐标变换关系就可以实现PP1和PP2之间的转换。

### Panorama

图像平面变换的一个典型应用是获得**全景图(panorama)**。我们可以利用图像平面的变换将不同角度拍摄的图像变换到一个固定的角度，从而获得更大的视野。

<div align=center>
<img src="https://i.imgur.com/vNAPQjy.png" width="70%">
</div>

全景图拼接的本质是把不同的成像平面变换到一个给定的平面上，从而得到空间点在该平面上的投影。因此这样的过程需要保证不同图像的成像中心是同一点，同时视野的角度需要小于180°，否则会产生一些扭曲的问题。

<div align=center>
<img src="https://i.imgur.com/Wl2B40P.png" width="20%">
</div>

### Homography

图像平面到图像平面的变换可以利用投影变换的单应矩阵$H$来描述，两幅图像上对应点的坐标满足：

$$
p' = H p
$$

由于单应矩阵$H$具有8个自由度，我们需要至少4组对应点才能求解。类似于计算相机矩阵的过程，我们可以假定$H$矩阵的最后一个元素为1来求解；而实际中更常用的方式是利用奇异值分解来计算，整个计算流程类似于[Direct Linear Calibration](/2021/09/14/OMSCS-CV-NOTES-07.html#direct-linear-calibration)。

## Projective Geometry

## Essential matrix

## Fundamental matrix
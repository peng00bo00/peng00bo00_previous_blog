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

## Projective Geometry

## Essential matrix

## Fundamental matrix
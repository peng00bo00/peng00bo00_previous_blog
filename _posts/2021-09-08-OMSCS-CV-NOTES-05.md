---
layout: article
title: OMSCS-CV课程笔记05-Stereo Geometry
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-05
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍立体视觉的相关内容。
<!--more-->

## Stereo Geometry

在相机的成像过程中我们去掉了空间点的z坐标，也就是说我们无法只通过单一图像来获知空间点的深度信息。更严重的问题是如果存在两个点P1和P2与投影中心共线，在投影后它们会具有相同的坐标而且我们没有办法对它们进行区分。

<div align=center>
<img src="https://i.imgur.com/n8RlZjm.png" width="50%">
</div>

因此仅通过单张图像去还原物体的空间信息是非常困难的。要解决这个问题最简单的方法是添加一个额外的相机，用两个相机来还原物体的空间信息。实际上人眼感知空间也是利用了类似的原理，当我们用双眼观察物体时两只眼睛的观察结果会有微小的差异，这个微小的差异就产生了物体的空间感。

最基本的立体视觉系统由两个相机组成，我们称为**双目视觉(stereo vision)**。对于空间中的点P假设我们知道它在两张图像上的位置以及两个相机的位姿，我们就可以利用图像还原出P点在空间中的坐标。

<div align=center>
<img src="https://i.imgur.com/UEBdY5o.png" width="70%">
</div>

双目视觉的经典应用是空间点的**深度估计(depth estimation)**。假设我们有两个平行放置焦距为$f$的相机，它们投影中心的距离为B称为**基线(baseline)**。此时空间点P与两个投影中心构成了一个平面如图下图所示：

<div align=center>
<img src="https://i.imgur.com/XfX5Yv0.png" width="40%">
</div>

记P的深度为$Z$，它在两张图像上的横坐标分别为$x_l$和$x_r$。根据相似三角形可以得到几何关系：

$$
\frac{B}{Z} = \frac{B-x_l+x_r}{Z-f} = \frac{x_l-x_r}{f}
$$

因此深度可以表示为：

$$
Z = \frac{B}{x_l-x_r} f
$$

其中$x_l-x_r$表示P点在两张图像上横坐标的差异，称为**视差(disparity)**。对于同一个双目相机，视差越小表明该点到相机的距离越远。描述图像上每一点视差的图片称为**视差图(disparity map)**。

<div align=center>
<img src="https://i.imgur.com/oVJhB8U.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/PxpRpoM.png" width="80%">
</div>

## Epipolar Geometry

在大部分实际应用中我们很难保证两个相机相互平行，此时利用图像还原空间信息会相对困难一些。

<div align=center>
<img src="https://i.imgur.com/C24pXGH.png" width="80%">
</div>

设空间点P在两张图像上的投影分别为$p$和$p'$。P点与两个投影中心构成了一个平面称为**极平面(epipolar plane)**，极平面与投影平面的交线称为**极线(epipolar line)**，基线与投影平面的交点称为**极点(epipole)**。根据几何关系不难发现极平面上的点会被投影到成像平面的极线上，此外同一投影平面上所有的极线都交于极点。极点、极线和极平面之间的关系称为**对极约束(epipolar constraint)**。

<div align=center>
<img src="https://i.imgur.com/0opuZb6.png" width="60%">
</div>

对极约束的一个直接应用是加速图像上点的匹配：对于图像上的任一点在寻找匹配时无需在另一张图像上进行遍历，根据对极约束我们只需要在极线上进行搜索即可，这样大大加快了匹配的过程。

<div align=center>
<img src="https://i.imgur.com/lhbFEwV.png" width="70%">
</div>

当两个相机相互平行时，极线会变成图像中相互平行的水平直线。此时极点位于成像平面的无穷远处。

<div align=center>
<img src="https://i.imgur.com/fF306IR.png" width="60%">
</div>

<div align=center>
<img src="https://i.imgur.com/N6tFdY1.png" width="70%">
</div>

## Stereo Correspondence
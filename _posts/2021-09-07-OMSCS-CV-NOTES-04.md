---
layout: article
title: OMSCS-CV课程笔记04-Camera Models
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-04
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍相机模型的相关内容。
<!--more-->

## Cameras and Images

在图像处理中我们把图像视为一种二维函数，但现实生活中的图像不仅仅是一个二维函数。实际上图像是三维空间中的点在二维平面上的投影，我们通过相机来将三维空间中的点投影到平面上。

### Pinhole Camera

现实生活中最简单的相机是**针孔相机(pinhole camera)**，它通过小孔成像的原理将空间中的点投影到底片上。

<div align=center>
<img src="https://i.imgur.com/B5LMp0N.png" width="70%">
</div>

针孔相机的一个主要问题在于成像不够清晰，这通常是由于针孔的尺寸取得过大所导致的。当针孔比较大时同一点发出的不同光线会投影到底片的不同位置，来自不同物体的光线在同一位置上相互叠加就会导致成像变得模糊。同时需要说明的是针孔的尺寸并不是越小越好，当针孔过于小时由于光的衍射(diffraction)也可能会导致成像的模糊。

<div align=center>
<img src="https://i.imgur.com/YYglSfz.png" width="70%">
</div>

### Lenses

实际中更常用的相机是带镜头的相机，我们利用镜头来将光线汇聚到底片上。通常情况下我们假定镜头是足够薄，这样可以得到**成像公式(thin lens equation)**：

$$
\frac{1}{z} + \frac{1}{Z} = \frac{1}{f}
$$

<div align=center>
<img src="https://i.imgur.com/9nNf5pC.png" width="50%">
</div>

当相机和透镜确定时，**光圈(aperture)**的大小控制了**景深(depth of field)**的范围。当光圈比较大时会有较多的光线进入透镜，此时的景深较小；相反的当光圈比较小时只会有少部分的光线进入透镜，此时的景深会增大。

<div align=center>
<img src="https://i.imgur.com/jR2KTF0.png" width="50%">
</div>

<div align=center>
<img src="https://i.imgur.com/DaRkn9B.png" width="40%">
<img src="https://i.imgur.com/2wKpATI.png" width="40%">
</div>

在成像过程中另一个重要参数是**视野(field of view)** $\phi$，它与焦距$f$以及底片尺寸$d$有关。当底片尺寸确定时焦距越大，视野越小。

$$
\phi = \tan^{-1} \bigg( \frac{d}{2 f} \bigg)
$$

<div align=center>
<img src="https://i.imgur.com/NlwWGhp.png" width="50%">
</div>

<div align=center>
<img src="https://i.imgur.com/gKarQoK.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/AaMVHWm.png" width="80%">
</div>

直观上理解视野描述了成像区域的大小，视野越大成像的范围就越大。但需要注意的是调整视野和调整成像距离是不完全一致的，这在人像摄影中尤为重要。

<div align=center>
<img src="https://i.imgur.com/Lzrct7A.png" width="70%">
</div>

<div align=center>
<img src="https://i.imgur.com/xvp4j9P.png" width="70%">
</div>

此外，焦距还会对透视产生一定的影响。当焦距不断增大时，成像的结果会趋向于平行投影。

<div align=center>
<img src="https://i.imgur.com/4RD9spN.png" width="70%">
</div>

焦距的在成像中的另一个应用是滑动变焦(dolly zoom)。只需要改变焦距和成像距离而无需移动物体就可以干扰人眼对空间的认知，这在很多影视作品中都有应用。

<div align=center>
<img src="https://upload.wikimedia.org/wikipedia/commons/c/c7/Contra-zoom_aka_dolly_zoom_animation.gif" width="40%">
</div>

现实生活中的透镜由于制造工艺等因素会存在一定的缺陷，其中最常见的缺陷是畸变(distortion)，此时原本的直线在投影后会变成曲线：

<div align=center>
<img src="https://i.imgur.com/WUKSPF8.png" width="50%">
</div>

<div align=center>
<img src="https://i.imgur.com/t0NdfnY.png" width="32%">
<img src="https://i.imgur.com/jJvUc0j.png" width="47%">
</div>

另一种常见的缺陷是**色差(chromatic aberration)**，它是指透镜无法将各种波长的色光都聚焦在同一点上的现象。

<div align=center>
<img src="https://i.imgur.com/kYJjhQt.png" width="70%">
</div>

<div align=center>
<img src="https://upload.wikimedia.org/wikipedia/commons/6/66/Chromatic_aberration_%28comparison%29.jpg" width="40%">
</div>

此外还可能会出现**晕影(vignetting)**的现象：由于镜筒的存在倾斜入射的光线比垂直入射的光线要少一些，使得图像的边缘比中心显得更暗。

<div align=center>
<img src="https://photographylife.com/wp-content/uploads/2013/10/Optical-Vignetting.png" width="50%">
</div>

<div align=center>
<img src="https://i.imgur.com/tPn2fhx.png" width="70%">
</div>

## Perspective Imaging
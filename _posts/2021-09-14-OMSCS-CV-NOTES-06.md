---
layout: article
title: OMSCS-CV课程笔记06-Camera Calibration
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-06
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍相机标定的相关内容。
<!--more-->

## Geometric Camera Calibration

在[Camera Models](/2021/09/07/OMSCS-CV-NOTES-04.html#modeling-projection)一节中我们介绍了齐次坐标和相机的投影模型，从而将三维空间中的点投影到图像平面上。本节课中我们会把这个方法推广到更一般的情形中：我们不再假定坐标原点位于相机的投影中心，而是将任意坐标系下的点投影到图像平面上。我们把确定空间坐标与图像坐标之间关系的过程称为**相机的几何标定(geometric camera calibration)**，简称相机标定。

相机标定包括2部分内容：

1. 世界坐标到相机坐标的变换，这部分称为相机的**外参数(extrinisic parameters)**或**位姿(pose)**。
2. 相机坐标到图像坐标的变换，这部分称为相机的**内参数(intrinisic parameters)**。

## Extrinsic Camera Calibration

世界坐标到相机坐标的变换是三维空间点的刚体变换，一共有6个外参数：3个平移+3个旋转。

<div align=center>
<img src="https://i.imgur.com/q2OohzA.png" width="70%">
</div>

### Translation

空间点$P$在坐标系$A$中的坐标可以写成基矢量和的形式：

$$
^AP = (^Ax, ^Ay, ^Az) = ^Ax \cdot i_A + ^Ay \cdot j_A + ^Az \cdot k_A
$$

<div align=center>
<img src="https://i.imgur.com/7dTllok.png" width="40%">
</div>

假设空间中还存在另一个坐标系$B$，它与$A$只相差一个平移。根据矢量加法$P$点在坐标系$B$中的坐标为：

$$
^BP = ^B(O_A) + ^AP
$$

其中$^B(O_A)$表示$A$坐标系中的原点$O_A$在$B$坐标系中的坐标。

<div align=center>
<img src="https://i.imgur.com/MkKRUPH.png" width="70%">
</div>

我们利用齐次坐标来重写上式可以得到平移变换的矩阵形式：

$$
\begin{bmatrix}
^BP \\ 1
\end{bmatrix}
=
\begin{bmatrix}
I_{3 \times 3} & ^B(O_A) \\
0^T & 1
\end{bmatrix}
\begin{bmatrix}
^AP \\ 1
\end{bmatrix}
$$

### Rotation

对于刚体旋转，我们分别取$P$点在两个坐标系下的表示为：

$$
P = 
\begin{bmatrix}
i_A & j_A & k_A
\end{bmatrix}
\begin{bmatrix}
^Ax \\ ^Ay \\ ^Az
\end{bmatrix}
=
\begin{bmatrix}
i_B & j_B & k_B
\end{bmatrix}
\begin{bmatrix}
^Bx \\ ^By \\ ^Bz
\end{bmatrix}
$$

<div align=center>
<img src="https://i.imgur.com/kMAzvq3.png" width="40%">
</div>

因此我们可以得到刚体旋转的坐标变换公式：

$$
^BP = ^B_AR \ ^AP
$$

$$
^B_AR
= 
\begin{bmatrix}
i_A \cdot i_B & j_A \cdot i_B & k_A \cdot i_B \\
i_A \cdot j_B & j_A \cdot j_B & k_A \cdot j_B \\
i_A \cdot k_B & j_A \cdot k_B & k_A \cdot k_B \\
\end{bmatrix}
=
\begin{bmatrix}
^Bi_A & ^Bj_A & ^Bk_A
\end{bmatrix}
=
\begin{bmatrix}
{^Ai_B}^T \\ {^Aj_B}^T \\ {^Ak_B}^T
\end{bmatrix}
$$

其中$^Bi_A$表示$A$坐标系的基矢量$i_A$在$B$坐标系中的坐标。我们称$^B_AR$为$A$坐标系到$B$坐标系的旋转矩阵，它的第i行j列元素为$B$坐标系第j个基矢量与$A$坐标系第i个基矢量的内积。同时需要注意的是旋转矩阵是一个正交阵，即$R^T R = I$。

### Rigid Transformations

## Instrinsic Camera Calibration

## Calibrating Cameras
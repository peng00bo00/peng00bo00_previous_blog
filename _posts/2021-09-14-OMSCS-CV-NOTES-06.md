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

其中$^Bi_A$表示$A$坐标系的基矢量$i_A$在$B$坐标系中的坐标。我们称$^B_AR$为$A$坐标系到$B$坐标系的旋转矩阵，它的第i行j列元素为$B$坐标系第j个基矢量与$A$坐标系第i个基矢量的内积。同时需要注意的是旋转矩阵是一个**正交阵(orthogonal matrix)**即$R^T R = I$，而且旋转矩阵不具有交换性$R_1 R_2 \neq R_2 R_1$。

类似于平移变换，我们同样可以把刚体旋转用齐次坐标来表示，从而得到矩阵形式：

$$
\begin{bmatrix}
^BP \\ 1
\end{bmatrix}
=
\begin{bmatrix}
^B_AR & 0 \\
0^T & 1
\end{bmatrix}
\begin{bmatrix}
^AP \\ 1
\end{bmatrix}
$$

### Rigid Transformations

我们把平移和旋转组合到一起就得到了刚体变换公式：

$$
^BP = ^B_AR \ ^AP + ^B O_A
$$

<div align=center>
<img src="https://i.imgur.com/oEcdNCI.png" width="70%">
</div>

同样利用齐次坐标可以得到矩阵形式：

$$
\begin{bmatrix}
^BP \\ 1
\end{bmatrix}
=
\begin{bmatrix}
I_{3 \times 3} & ^BO_A \\
0^T & 1
\end{bmatrix}
\begin{bmatrix}
^B_AR & 0 \\
0^T & 1
\end{bmatrix}
\begin{bmatrix}
^AP \\ 1
\end{bmatrix}
=
\begin{bmatrix}
^B_AR & ^BO_A \\
0^T & 1
\end{bmatrix}
\begin{bmatrix}
^AP \\ 1
\end{bmatrix}
$$

我们记矩阵$^B_AT=\begin{bmatrix}^B_AR & ^B(O_A) \\ 0^T & 1 \end{bmatrix}$为坐标系$A$到坐标系$B$的刚体变换矩阵，它的逆阵$^A_BT = {^B_AT}^{-1}$为坐标系$B$到坐标系$A$的刚体变换矩阵。当我们取$A$为世界坐标系同时取$B$为相机坐标系时，$^B_AT$表示世界坐标到相机坐标的变换，因此也称其为相机的**外参数矩阵(extrinsic parameter matrix)**。显然外参数矩阵是一个$4\times4$的可逆矩阵，它具有3个旋转自由度和3个平移自由度。

## Instrinsic Camera Calibration

### Real Intrinsic Parameters

接下来考虑相机坐标系投影到图像坐标系的过程。对于理想情况下的针孔相机模型，我们只需要知道相机的焦距就可以完成投影：

$$
u = f \frac{x}{z}
$$

$$
v = f \frac{y}{z}
$$

<div align=center>
<img src="https://i.imgur.com/iOtIdbv.png" width="60%">
</div>

然而现实中相机的投影并不会这样完美。首先图像上的像素坐标没有物理意义也不代表现实中的长度，同时$u$、$v$两个方向上单位像素的长度也不一定严格相等。因此我们不能够直接使用焦距$f$来表示投影过程，而是需要引入2个方向上的待定参数$\alpha$和$\beta$：

$$
u = \alpha \frac{x}{z}
$$

$$
v = \beta \frac{y}{z}
$$

另一方面，按照上式进行投影后图像的原点会位于图像的中心。但在图像处理中图像的原点并不在图像中心，因此我们需要考虑将投影后相机的原点进行平移：

$$
u = \alpha \frac{x}{z} + u_0
$$

$$
v = \beta \frac{y}{z} + v_0
$$

此外，如果$u$和$v$两个方向不是严格垂直的话投影公式会变得更加复杂：

$$
u = \alpha \frac{x}{z} - \alpha \frac{y}{z} \cot (\theta) + u_0
$$

$$
v = \frac{\beta}{\sin (\theta)} \frac{y}{z} + v_0
$$

<div align=center>
<img src="https://i.imgur.com/Jlna2vV.png" width="60%">
</div>

我们将整个投影过程用齐次坐标来表达就得到了相机的**内参数矩阵(intrinsic matrix)** $K$：

$$
\begin{bmatrix}
z \cdot u \\ z \cdot v \\ z
\end{bmatrix}
=
\begin{bmatrix}
\alpha & -\alpha \cot (\theta) & u_0 & 0 \\
0 & \frac{\beta}{\sin (\theta)} & v_0 & 1 \\
0 & 0 & 1 & 0
\end{bmatrix}

\begin{bmatrix}
x \\ y \\ z \\ 1
\end{bmatrix}
$$

$$
p' = K \  ^Cp
$$

利用齐次坐标的另一个好处是我们可以去掉矩阵的最后一列，得到更常见的内参数矩阵形式：

$$
K = 
\begin{bmatrix}
f & s & c_x \\
0 & a f & c_y \\
0 & 0 & 1
\end{bmatrix}
$$

其中$f$为焦距；$s$表示坐标轴的倾斜程度，在理想情况下为0；$c_x$和$c_y$为图像坐标系原点的偏移量；$a$为像素的长宽比，理想条件下为1.0。显然相机的内参数矩阵$K$一共有5个自由度。

### Camera Parameters

我们把相机的外参数矩阵、投影矩阵以及内参数矩阵组合到一起就得到了相机矩阵，它表示世界坐标系到图像坐标系的变换过程。

<div align=center>
<img src="https://i.imgur.com/UWsPQGv.png" width="70%">
</div>

从前面的推导不难发现相机矩阵一共有11个自由度：其中6个来自于外参数矩阵(3个平移+3个旋转)，另外5个来自于内参数矩阵。需要注意的是直接使用相机矩阵得到的坐标是图像平面上的齐次坐标，需要对最后一维进行归一化才能得到所需的像素坐标。

## Calibrating Cameras
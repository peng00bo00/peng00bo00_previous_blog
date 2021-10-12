---
layout: article
title: OMSCS-CV课程笔记10-Motion Detection
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-10
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍运动估计和光流的相关内容。
<!--more-->

## Image Motion

在前面的课程中我们介绍了如何对单张图像进行处理，而从本节课开始我们将讨论对视频和图像序列进行分析和处理。其中，**运动检测(motion detection)**是视频分析的基本内容。对于输入的图像序列我们希望得到图像中物体的运动信息，进而实现各种视觉任务。

运动检测主要分为两类，一种是基于特征点的检测而另一种则是基于光度的检测。在前面的课程中我们已经涉及了图像特征点的内容，我们可以在图像序列上对每帧图像都进行特征点识别然后对这些特征点进行跟踪从而完成运动检测。这类方法适用于图像发生大变形的场景，但缺点是只能得到稀疏的检测结果。而本节课则主要介绍第二种方法，即基于光度信息的运动检测。与第一种方法相反，它只适用于图像变化比较小的场景但却可以得到稠密的检测结果。

## Optical Flow

### Brightness Constraint

光流(optical flow)是实现稠密运动检测的基本方法。当图像运动较小时，我们可以通过光流来得到图像上每一点的运动状况。

<div align=center>
<img src="https://i.imgur.com/lCeJJK0.png" width="90%">
</div>

光流法的目标是估计图像上每一点的运动状态，在具体推导光流前我们首先需要做出2个基本假设：

1. **光度一致(brightness constancy)**：同一个点在不同图像上具有相同的光度(颜色)；
2. 小变形：图像上的任意点在运动前后不会发生比较大的位置变化。

基于光度一致假设，我们可以得到方程：

$$
I(x, y, t) = I(x+u, y+v, t+1) \Leftrightarrow I(x+u, y+v, t+1) - I(x, y, t) = 0
$$

<div align=center>
<img src="https://i.imgur.com/pI2SEaf.png" width="70%">
</div>

利用泰勒展开，我们可以把$t+1$时刻的图像表示为：

$$
I(x+u, y+v, t+1) \approx I(x, y, t+1) + I_x u + I_y v
$$

这样得到**光度一致约束方程(brightness constancy constraint equation)**：

$$
\begin{aligned}
0 &= I(x+u, y+v, t+1) - I(x, y, t) \\
&= I(x, y, t+1) + I_x u + I_y v - I(x, y, t) \\
&= I_t + I_x u + I_y v
\end{aligned}
$$

### LK Optical Flow

接下来的问题是如何求解这个方程。对于图像上的任意点我们可以计算光度值的导数$I_x, I_y, I_t$，但此时我们有2个未知数却只有一个方程。一种直观的解决方法是把每个点的邻域也考虑进来，构造一个超定方程来求解。假设我们考虑每个点周围$5 \times 5$的邻域，我们可以得到方程组：

$$
\begin{bmatrix}
I_x(p_1) & I_y(p_1) \\
I_x(p_2) & I_y(p_2) \\
\vdots & \vdots \\
I_x(p_{25}) & I_y(p_{25})
\end{bmatrix}

\begin{bmatrix}
u \\ v
\end{bmatrix}
= 
-
\begin{bmatrix}
I_t(p_1) \\ I_t(p_2) \\ \vdots \\ I_t(p_{25})
\end{bmatrix}

\Leftrightarrow
A d = b
$$

对于这样的方程组我们使用它的最小二乘解：

$$
(A^T A) d = A^T b
$$

更常见的形式为：

$$
\begin{bmatrix}
\sum I_x I_x & \sum I_x I_y \\
\sum I_y I_x & \sum I_y I_y \\
\end{bmatrix}

\begin{bmatrix}
u \\ v
\end{bmatrix}
= 

\begin{bmatrix}
-\sum I_x I_t \\ -\sum I_y I_t
\end{bmatrix}
$$

这种方法最早由Lukas和Kanade于1981年提出，因此求解这个方程得到的光流也称为LK光流。除此之外，LK光流还提出了通过迭代来处理图像运动过大的问题：当图像运动过大时首先估计一个粗糙的解，然后把运动后的图像按照这个解反变换到运动前的状态再次进行运动估计。如此反复迭代从而得到一个更加准确的运动估计：

<div align=center>
<img src="https://i.imgur.com/VbJpNdm.png" width="70%">
</div>

<div align=center>
<img src="https://i.imgur.com/e1YmPUb.png" width="70%">
</div>

<div align=center>
<img src="https://i.imgur.com/MX5DC4V.png" width="70%">
</div>

### Hierarchical LK

LK光流的一个主要问题在于混淆(aliasing)：在很多情况下计算得到的解只是最近的解但并不是真实的解。

<div align=center>
<img src="https://i.imgur.com/tDniTqT.png" width="70%">
</div>

实际工程中一般会通过多尺度的方法来处理这个问题：从高尺度出发首先估计一个粗糙的解，然后逐步缩小尺度并对粗糙解进行更新，直到获得一个精准的解。

<div align=center>
<img src="https://i.imgur.com/H0ysJHB.png" width="70%">
</div>

在介绍多尺度光流前我们首先引入多尺度的概念。在[Aliasing](/2021/08/31/OMSCS-CV-NOTES-03.html#aliasing)一节中我们介绍过利用高斯模糊来处理对图像进行降采样时产生的走样问题。

<div align=center>
<img src="https://i.imgur.com/VgzTvqp.png" width="70%">
</div>

我们对同一张图像不断地使用高斯模糊和降采样进行处理，就能够得到一个图像序列称为**高斯金字塔(Gaussian pyramid)**：

<div align=center>
<img src="https://i.imgur.com/GxPL03S.png" width="70%">
</div>

在高斯金字塔中原始图像位于最底层，每向上前进一层图像的常和宽就缩减为原来的1/2。因此高斯金字塔实际上就是同一张图像在不同尺度(分辨率)下的不同表示，层数越高对应的尺度越大图像也就越模糊。

另一种常用的图像金字塔是**拉普拉斯金字塔(Laplacian pyramid)**。它的构造过程与高斯金字塔相同，但在存储时保留最顶层的图像高尺度图像以及每一层与相邻层的差，也就是DoG算子的运算结果。由于高斯滤波是一个低通滤波器，图像与它经过滤波后的差对应原始图像的高频成分，因此我们也可以认为拉普拉斯金字塔存储了图像在不同频段上的信息。

<div align=center>
<img src="https://i.imgur.com/1OblycC.png" width="70%">
</div>

拉普拉斯金字塔的具体构造过程如下：我们把原始图像放在$G_0$层，然后自下而上利用Reduce操作得到一系列长宽减半的图像序列$G_1, G_2, ...$；然后对于这些高层的图像再利用Expand操作恢复分辨率并与下一层图像作差得到拉普拉斯金字塔$L_0, L_1, L_2, ...$

<div align=center>
<img src="https://i.imgur.com/4QqPIMu.png" width="70%">
</div>
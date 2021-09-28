---
layout: article
title: OMSCS-CV课程笔记08-Feature and Matching
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-08
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍图像特征与匹配的相关内容。
<!--more-->

## Feature Detection

### Introduction to Features

在前面的课程中我们已经介绍过如何对图像进行几何变换，我们可以通过两幅图像上对应点的坐标来将其中一幅图像变换到另一幅图像上，而在本节课中我们将介绍如何寻找这样的特征点以及对图像上的特征点进行匹配。通常情况下图像的特征点包含两部分：特征点的坐标和相应的**描述子(descriptor)**。对于不同图像中的同一个点，它在不同图像上的坐标互不相同但都具有相似的描述子。理想情况下特征点的描述子需要具有以下特性：

- Repeatability/Precision：同样的特征在几何和光照变换下保持不变；
- Saliency/Matchability：所有的特征都是独一无二的；
- Compactness and Efficiency：描述子需要足够简洁，数量要远小于图像像素数；
- Locality：描述子表达了图像的局部性质，并且对遮挡有足够的鲁棒性。

<div align=center>
<img src="https://i.imgur.com/Km7h6Us.png" width="70%">
</div>

### Corner Detection

**角点(corner)**是最基本的图像特征，它指的是在图像的各个方向上都有显著变化的像素点。

<div align=center>
<img src="https://i.imgur.com/5fKhGq9.png" width="70%">
</div>

从数学上来看，假设我们对图像上的点进行一个微小的平移$(u, v)$，平移前后图像像素值的变化可以表示为：

$$
E(u, v) = \sum_{x, y} w(x, y) [I(x+u, y+v) - I(x, y)]^2
$$

其中$w(x,y)$为窗口函数，它表示邻域像素点对于中心像素贡献的权重，一般可取常数1或高斯函数。显然位移$(u,v)$越大，像素变化越大；当$(u,v) = (0, 0)$时像素的变化值为$E(0, 0) = 0$。

<div align=center>
<img src="https://i.imgur.com/Nj3DVL6.png" width="50%">
</div>

由于角点是图像的局部特征，我们更关心$E(u, v)$在原点附近的变化情况。因此利用泰勒公式在原点附近展开：

$$
E(u, v) \approx E(0, 0) + 
\begin{bmatrix}
E_u(0, 0) & E_v(0, 0)
\end{bmatrix}
\begin{bmatrix}
u \\ v
\end{bmatrix} + 
\frac{1}{2} 
\begin{bmatrix}
u & v
\end{bmatrix}
\begin{bmatrix}
E_{uu}(0, 0) & E_{uv}(0, 0) \\
E_{vu}(0, 0) & E_{vv}(0, 0)
\end{bmatrix}
\begin{bmatrix}
u \\ v
\end{bmatrix}
$$

对原始公式进行求导可以得到：

$$
E_u (u, v) = \sum_{x, y} 2 w(x, y) [I(x+u, y+v) - I(x, y)] I_x(x+u, y+v)
$$

$$
E_u (0, 0) = E_v (0, 0)  = 0
$$

类似地，可以证明Hessian矩阵满足：

$$
E_{uu} (0, 0) = \sum_{x, y} 2 w(x, y) I_x(x, y) I_x(x, y)
$$

$$
E_{vv} (0, 0) = \sum_{x, y} 2 w(x, y) I_y(x, y) I_y(x, y)
$$

$$
E_{uv} (0, 0) = E_{vu} (0, 0) = \sum_{x, y} 2 w(x, y) I_x(x, y) I_y(x, y)
$$

把它们代回原式可以得到化简后的形式：

$$
E(u, v) \approx 
\begin{bmatrix}
u & v
\end{bmatrix}
M
\begin{bmatrix}
u \\ v
\end{bmatrix}
$$

$$
M = \sum_{x, y} w(x, y)
\begin{bmatrix}
I_x I_x & I_x I_y \\
I_x I_y & I_y I_y
\end{bmatrix}
$$

矩阵$M$也称为图像的**二阶矩矩阵(second moment matrix)**。二阶矩矩阵$M$的两个主方向对应图像梯度变化最大和最小的两个方向，对应的特征值表示变化的剧烈程度。如果两个特征值都接近于0，说明图像在所有的方向上变化都不明显，对应比较平坦的区域；如果两个特征值都很大，说明图像在所有的方向上都有剧烈的变化，即为所需的角点。

在Harris角点检测算法中定义了响应值$R$来判断某个点是否是角点：

$$
\begin{aligned}
R &= \lambda_1 \lambda_2 - \alpha \cdot (\lambda_1 + \lambda_2)^2 \\
&= \det (M) - \alpha \cdot \text{tr}^2 (M) \\
\end{aligned}
$$

其中$\alpha$为一个常数，一般取$\alpha$介于0.04~0.06。当响应值$R$大于指定的阈值时即可认为是一个可能的角点，而在实际中往往还会结合非极大值抑制来筛选出局部极值作为最终的角点。

<div align=center>
<img src="https://i.imgur.com/nHpkDzl.png" width="30%">
</div>

综合以上所有的步骤，得到Harris角点检测算法流程如下：

<div align=center>
<img src="https://i.imgur.com/cezLQYM.png" width="80%">
</div>

### Scale Invariance

图像角点对于平移、旋转以及光照变化都具有一定的不变性，但对于尺度变换却不具有不变性。简单来说当我们对图像进行缩放时，图像的边缘部分可能会转换成角点；而当我们对图像进行放大时，原来的角点则可能会转换成边缘。

<div align=center>
<img src="https://i.imgur.com/wHmtQVl.png" width="70%">
</div>

显然我们希望图像的特征点对于尺度变换也具有一定的不变性，为此我们首先需要对"尺度"进行定义。所谓"尺度"可以理解成图像的邻域性质，我们可以在不同的图像上使用尺寸不同的邻域进行观察，同样的特征应该会得到相同的结果。

<div align=center>
<img src="https://i.imgur.com/hByCzs6.png" width="50%">
</div>

接下来我们的问题就是如何在不同的图像上选择相应的邻域尺寸。一种解决办法是把特征定义成一个与邻域尺寸有关的函数，然后在不同大小的邻域上计算它，这样我们总能在某个尺度上找到所需的特征。同时这样的特征还需要在对应尺度上有稳定的响应，这样我们就可以把它在不同尺度上响应的最大值作为尺度不变的特征。

实践中一般可以通过图像卷积来构造尺度不变特征，比较常用的卷积核包括LoG算子(Laplacian of Gaussian)和DoG算子(Difference of Gaussians)：

$$
LoG = \sigma^2 (G_{xx} (x, y, \sigma) + G_{yy} (x, y, \sigma))
$$

$$
DoG = G(x, y, k \sigma) - G(x, y, \sigma)
$$

<div align=center>
<img src="https://i.imgur.com/f4IAqeI.png" width="40%">
</div>

其中不同的方差项$\sigma$对应不同的尺度。这样在特征点检测时同时在不同尺度上的每张图像都进行检测并在不同尺度上选择最大响应的特征就构造出了尺度不变的特征点。比如说Harris-Laplacian角点检测算法中利用LoG算子来构造尺度空间，它要求角点不仅要在图像空间上是局部极值还要在相邻尺度上也是一个局部极值，这样使得检测出的角点也具有尺度不变性。

<div align=center>
<img src="https://i.imgur.com/z74t3TC.png" width="50%">
</div>

## Feature Descriptors

## Feature Robustness
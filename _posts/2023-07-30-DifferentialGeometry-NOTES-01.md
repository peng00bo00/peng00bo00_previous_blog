---
layout: article
title: 微分几何笔记01-预备知识
tags: ["CG", "Geometry Processing", "Math"]
key: DifferentialGeometry-01
aside:
  toc: true
sidebar:
  nav: DifferentialGeometry
---

> 这个系列以北京大学陈维桓教授《微分几何(第二版)》为教材记录一下微分几何的学习过程，主要涉及古典微分几何中曲线曲面理论的相关知识。系统地学习微分几何对于理解和设计几何处理算法是十分有益的。
<!--more-->

## 三维欧式空间中的标架

### 向量运算

古典微分几何主要研究三维欧式空间$$\mathbb{E}^3$$，其中的每一个元素称为**点**。空间中任意两个点$$A, B \in \mathbb{E}^3$$可以构造一条有向线段，记以$$A$$为起点$$B$$为终点的有向线段为$$\overrightarrow{AB}$$。设$$\overrightarrow{AB}$$和$$\overrightarrow{CD}$$为两条有向线段，如果$$ABCD$$构成一个平行四边形则称这两条线段是相等的，记为

$$
\overrightarrow{AB} = \overrightarrow{CD}
$$

而所有相等的有向线段构成的集合称为一个**向量**，通常使用斜黑体字母来表示如$$\boldsymbol{a}$$。

#### 加法

向量相加只需要将它们的首尾相接：记$$\overrightarrow{AB}$$和$$\overrightarrow{BC}$$两个向量分别为$$\boldsymbol{a}$$和$$\boldsymbol{b}$$，则连接$$A$$和$$C$$的有向线段$$\overrightarrow{AC}$$就代表向量$$\boldsymbol{a}+\boldsymbol{b}$$。除此之外，我们把起点和终点相同的有向线段集合称为零向量，记作$$\boldsymbol{0}$$。显然任何向量与零向量之和等于其自身：

$$
\boldsymbol{a}+\boldsymbol{0} = \boldsymbol{a}
$$

若向量$$\boldsymbol{a}$$表示有向线段$$\overrightarrow{AB}$$对应的向量，则有向线段$$\overrightarrow{BA}$$代表的向量可以记作$$-\boldsymbol{a}$$，因此有

$$
\boldsymbol{a}+(-\boldsymbol{a}) = \boldsymbol{0}
$$

我们把向量$$-\boldsymbol{a}$$称作$$\boldsymbol{a}$$的反向量。容易验证向量加法满足交换律和结合律：

$$
\boldsymbol{a}+\boldsymbol{b} = \boldsymbol{b}+\boldsymbol{a}
$$

$$
\boldsymbol{a}+(\boldsymbol{b}+\boldsymbol{c}) = (\boldsymbol{a}+\boldsymbol{b})+\boldsymbol{c}
$$

在$$\mathbb{E}^3$$中我们规定线段$$\overrightarrow{AB}$$的长度为点$$A$$到$$B$$的距离，记为$$\vert AB \vert$$。对于空间中的任意三点$$A$$，$$B$$，$$C$$，它们之间的距离需要满足三角不等式：

$$
\vert AB \vert + \vert BC \vert \geq \vert AC \vert
$$

当且仅当$$A$$，$$B$$，$$C$$三点共线时取等号。

#### 数乘

向量$$\boldsymbol{a}$$的长度$$\vert \boldsymbol{a} \vert$$表示它对应有向线段的长度，在此基础上我们可以定义**数乘**运算。对于任意实数$$c$$，它与向量$$\boldsymbol{a}$$的乘积$$c \cdot \boldsymbol{a}$$定义为与$$\boldsymbol{a}$$平行的向量。当$$c \gt 0$$时$$c \cdot \boldsymbol{a}$$与$$\boldsymbol{a}$$同向且其长度$$\vert c \cdot \boldsymbol{a} \vert$$为$$\vert \boldsymbol{a} \vert$$的$$c$$倍；类似地，当$$c \lt 0$$时$$c \cdot \boldsymbol{a}$$与$$\boldsymbol{a}$$反向且长度为$$\vert \boldsymbol{a} \vert$$的$$\vert c \vert$$倍；而当$$c = 0$$时$$c \cdot \boldsymbol{a} = \boldsymbol{0}$$。容易验证向量数乘运算满足如下性质：

$$
\lambda (\boldsymbol{a} + \boldsymbol{b}) = \lambda \boldsymbol{a} + \lambda \boldsymbol{b}
$$

$$
(\lambda + \mu) \boldsymbol{a} = \lambda \boldsymbol{a} + \mu \boldsymbol{a}
$$

$$
(\lambda \mu) \boldsymbol{a} = \lambda (\mu \boldsymbol{a})
$$

其中$$\lambda$$和$$\mu$$为任意实数。

#### 内积

向量和向量之间的内积(点乘)定义为实数

$$
\boldsymbol{a} \cdot \boldsymbol{b} = \vert \boldsymbol{a} \vert \cdot \vert \boldsymbol{b} \vert \cdot \cos{\angle(\boldsymbol{a}, \boldsymbol{b})}
$$

容易验证内积运算满足如下性质：

$$
\boldsymbol{a} \cdot \boldsymbol{b} = \boldsymbol{b} \cdot \boldsymbol{a}
$$

$$
\boldsymbol{c} \cdot (\boldsymbol{a} + \boldsymbol{b}) = \boldsymbol{c} \cdot \boldsymbol{a} + \boldsymbol{c} \cdot \boldsymbol{b}
$$

$$
(\lambda \boldsymbol{a}) \cdot \boldsymbol{b} = \lambda (\boldsymbol{a} \cdot \boldsymbol{b})
$$

实际上向量的长度也是由内积来定义的：

$$
\vert \boldsymbol{a} \vert^2 = \boldsymbol{a} \cdot \boldsymbol{a} \geq 0
$$

当且仅当向量$$\boldsymbol{a}$$为零向量$$\boldsymbol{0}$$时取等号。另外向量$$\boldsymbol{a}$$和$$\boldsymbol{b}$$垂直的充要条件为它们的内积为0：

$$
\boldsymbol{a} \cdot \boldsymbol{b} = 0 \Leftrightarrow \boldsymbol{a} \perp \boldsymbol{b}
$$

#### 叉乘

当向量$$\boldsymbol{a}$$和$$\boldsymbol{b}$$平行时规定它们的**叉乘**为零向量；而当它们不平行时，规定叉乘$$\boldsymbol{a} \times \boldsymbol{b}$$为与向量$$\boldsymbol{a}$$和$$\boldsymbol{b}$$都垂直的一个向量，其长度为$$\boldsymbol{a}$$和$$\boldsymbol{b}$$所张成的平行四边形面积：

$$
\vert \boldsymbol{a} \times \boldsymbol{b} \vert = \vert \boldsymbol{a} \vert \cdot \vert \boldsymbol{b} \vert \cdot \sin{\angle(\boldsymbol{a}, \boldsymbol{b})}
$$

且它和$$\boldsymbol{a}$$与$$\boldsymbol{b}$$构成右手系。容易验证叉乘运算满足如下性质：

$$
\boldsymbol{a} \times \boldsymbol{b} = -\boldsymbol{b} \times \boldsymbol{a}
$$

$$
\boldsymbol{c} \times (\boldsymbol{a} + \boldsymbol{b}) = \boldsymbol{c} \times \boldsymbol{a} + \boldsymbol{c} \times \boldsymbol{b}
$$

$$
(\lambda \boldsymbol{a}) \times \boldsymbol{b} = \lambda (\boldsymbol{a} \times \boldsymbol{b})
$$

根据定义，向量$$\boldsymbol{a}$$和$$\boldsymbol{b}$$相互平行的充要条件为它们的叉乘为零向量：

$$
\boldsymbol{a} \times \boldsymbol{b} = \boldsymbol{0} \Leftrightarrow \boldsymbol{a} \parallel \boldsymbol{b}
$$

### 正交标架

取$$\mathbb{E}^3$$空间中不共面的四个点，把其中一点记为$$O$$，其它三点分别记为$$A$$，$$B$$，$$C$$，于是得到一个由一点$$O$$和3个不共面向量$$\overrightarrow{OA}$$，$$\overrightarrow{OB}$$，$$\overrightarrow{OC}$$构成的图形$$\{O; \overrightarrow{OA}, \overrightarrow{OB}, \overrightarrow{OC} \}$$。这样的一个图形称为空间中的一个**标架**，点$$O$$称为该标架的**原点**。在给定标架$$\{O; \overrightarrow{OA}, \overrightarrow{OB}, \overrightarrow{OC} \}$$后，由原点指向空间中任意一点$$p$$的向量可以根据平行四边形法则唯一地表示为三个有序实数$$(x, y, z)$$：

$$
\overrightarrow{Op} = x \ \overrightarrow{OA} + y \ \overrightarrow{OB} + z \ \overrightarrow{OC}
$$

数组$$(x, y, z)$$称为点$$p$$关于标架$$\{O; \overrightarrow{OA}, \overrightarrow{OB}, \overrightarrow{OC} \}$$的坐标。

设$$\{O; \boldsymbol{i}, \boldsymbol{j}, \boldsymbol{k} \}$$是$$\mathbb{E}^3$$中的一个标架，且$$\boldsymbol{i}$$，$$\boldsymbol{j}$$，$$\boldsymbol{k}$$为彼此垂直并构成右手系的三个向量，则有

$$
\boldsymbol{i} \cdot \boldsymbol{i} = \boldsymbol{j} \cdot \boldsymbol{j} = \boldsymbol{k} \cdot \boldsymbol{k} = 1
$$

$$
\boldsymbol{i} \cdot \boldsymbol{j} = \boldsymbol{i} \cdot \boldsymbol{k} = \boldsymbol{j} \cdot \boldsymbol{k} = 0
$$

$$
\boldsymbol{i} \times \boldsymbol{j} = \boldsymbol{k}, \
\boldsymbol{j} \times \boldsymbol{k} = \boldsymbol{i}, \
\boldsymbol{k} \times \boldsymbol{i} = \boldsymbol{j}
$$

这样的标架称为**右手正交标架**，简称**正交标架**，而由正交标架给出的坐标系则称为笛卡尔直角坐标系。在笛卡尔直角坐标系下，设向量$$\boldsymbol{a}$$和$$\boldsymbol{b}$$的分量分别为$$(x_1, y_1, z_1)$$和$$(x_2, y_2, z_2)$$，则它们的内积和叉积可以表示为分量运算：

$$
\boldsymbol{a} \cdot \boldsymbol{b} = x_1 x_2 + y_1 y_2 + z_1 z_2
$$

$$
\boldsymbol{a} \times \boldsymbol{b} = 
\begin{vmatrix}
\boldsymbol{i} & \boldsymbol{j} & \boldsymbol{k} \\
x_1 & y_1 & z_1 \\
x_2 & y_2 & z_2 \\
\end{vmatrix}
$$

设点$$A$$和$$B$$的坐标分别为$$(x_1, y_1, z_1)$$和$$(x_2, y_2, z_2)$$，则线段$$AB$$的长度可以表示为：

$$
\vert AB \vert = \sqrt{\overrightarrow{AB} \cdot \overrightarrow{AB}}
= \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2 + (z_2 - z_1)^2}
$$

## 向量函数
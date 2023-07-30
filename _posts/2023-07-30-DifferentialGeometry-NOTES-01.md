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

向量$$\boldsymbol{a}$$的长度$$\vert \boldsymbol{a} \vert$$表示它对应有向线段的长度，在此基础上我们可以定义**数乘**运算。对于任意实数$$c$$，它与向量$$\boldsymbol{a}$$的乘积$c \cdot \boldsymbol{a}$定义为与$\boldsymbol{a}$平行的向量。当$$c \gt 0$$时$$c \cdot \boldsymbol{a}$$与$$\boldsymbol{a}$$同向且其长度$$\vert c \cdot \boldsymbol{a} \vert$$为$$\vert \boldsymbol{a} \vert$$的$$c$$倍；类似地，当$$c \lt 0$$时$$c \cdot \boldsymbol{a}$$与$$\boldsymbol{a}$$反向且长度为$$\vert \boldsymbol{a} \vert$$的$$\vert c \vert$$倍；当$$c = 0$$时$$c \cdot \boldsymbol{a} = \boldsymbol{0}$$。容易验证向量数乘运算满足如下性质：

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

### 正交标架

## 向量函数
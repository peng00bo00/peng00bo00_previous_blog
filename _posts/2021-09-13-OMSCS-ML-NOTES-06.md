---
layout: article
title: OMSCS-ML课程笔记06-SVM and Kernel Methods
tags: ["OMSCS", "CS7641-ML"]
key: OMSCS-ML-06
aside:
  toc: true
sidebar:
  nav: OMSCS-ML
---

> 这个系列是Gatech OMSCS 机器学习课程([CS 7641: Machine Learning](https://omscs.gatech.edu/cs-7641-machine-learning))的同步课程笔记。课程内容涉及监督学习、无监督学习和强化学习三个部分，本节主要介绍监督学习中支持向量机的相关内容。
<!--more-->

## Linear SVM

**支持向量机(support vector machine, SVM)**是经典的二分类模型。从几何的角度上讲，二分类问题可以理解为在空间中寻找一个**超平面(hyperplane)**来将数据划分为两部分。在数据集是线性可分的情况下存在无数个可行的超平面将数据集正确划分，如下图中的$H_2$和$H_3$所示。显然我们希望从这些超平面中选择一个"最好"的使得模型对于噪声和扰动都具有足够的鲁棒性。

<div align=center>
<img src="https://upload.wikimedia.org/wikipedia/commons/b/b5/Svm_separating_hyperplanes_%28SVG%29.svg" width="40%">
</div>

SVM通过最大化两个类别数据到超平面的距离来求解这个的超平面。假设超平面方程为$w^T x + b = 0$，对于正负样本有：

$$
\begin{aligned}
w^T x_i + b &\geq +1,  & &y_i = +1 \\
w^T x_i + b &\leq -1, & &y_i = -1 \\
\end{aligned}
$$

换句话说

$$
y_i (w^T x_i + b) \geq 1
$$

当且仅当$x_i$到超平面的距离最小时取等号，此时的$x_i$称为**支持向量(support vector)**。

对于任意点$x_i$，它到超平面的距离为：

$$
\gamma_i = \frac{y_i (w^T x_i + b)}{\Vert w \Vert}
$$

将支持向量带入上式可以得到正负两类样本到超平面的最小距离为：

$$
\gamma = \frac{2}{\Vert w \Vert} \sim \frac{1}{\Vert w \Vert^2}
$$

进而得到SVM对应的约束优化问题：

$$
\begin{aligned}
\max_{w, b} \ \ & \frac{1}{\Vert w \Vert^2} \\
\text{s.t.} \  \ & y_i (w^T x_i + b) \geq 1
\end{aligned}
$$

由于最大化$\frac{1}{\Vert w \Vert^2}$与最小化$\frac{1}{2} \Vert w \Vert^2$是等价的，因此更常见的SVM优化形式是：

$$
\begin{aligned}
\min_{w, b} \ \ & \frac{1}{2} \Vert w \Vert^2 \\
\text{s.t.} \  \ & y_i (w^T x_i + b) \geq 1
\end{aligned}
$$

## Kernel Methods

## Back to Boosting

## Reference

- 第7章：支持向量机，统计学习方法（第2版）
- [Wikipedia: Support-vector machine](https://en.wikipedia.org/wiki/Support-vector_machine)
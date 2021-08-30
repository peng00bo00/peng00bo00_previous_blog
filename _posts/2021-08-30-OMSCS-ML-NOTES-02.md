---
layout: article
title: OMSCS-ML课程笔记02-Regression
tags: ["OMSCS", "ML"]
key: OMSCS-ML-02
aside:
  toc: true
sidebar:
  nav: OMSCS-ML
---

> 这个系列是Gatech OMSCS 机器学习课程([CS 7641: Machine Learning](https://omscs.gatech.edu/cs-7641-machine-learning))的同步课程笔记。课程内容涉及监督学习、无监督学习和强化学习三个部分，本节主要介绍监督学习中回归问题的相关内容。
<!--more-->

## Linear Regression

监督学习是利用给定的数据(特征)$X$与去预测因变量$y$，当$y$为连续型变量时则称此时的问题是一个**回归(regression)**问题。对于回归问题最基本的算法是线性回归(linear regression)，此时我们假定因变量$y$是特征$X$的线性组合：

$$
y = X_1 \beta_1 + X_2 \beta_2 + \cdots + X_p \beta_p = X \beta
$$

其中$\beta$为组合系数。在某些情况下还需要考虑一个偏置项$\beta_0$，此时只需要对$X$进行増广即可：$X = [1, X_1, ..., X_p]^T$。

<div align=center>
<img src="https://i.imgur.com/SuWVYEL.png" width="50%">
</div>

线性回归的目标是求解出合适的组合系数$\beta$使得总体误差最小，最常用的方法是使用**最小二乘法(least square)**来进行求解，此时的误差为样本预测值与实际值之差的平方和：

$$
\text{RSS}(\beta) = \sum_{i=1}^N ( y_i - X_i \beta )^2 = (\mathbf{y} - \mathbf{X} \beta)^T (\mathbf{y} - \mathbf{X} \beta)
$$

上式说明误差$\text{RSS}(\beta)$是关于系数$\beta$的二次型。对$\text{RSS}(\beta)$求导并令导数为0得到：

$$
\mathbf{X}^T (\mathbf{y} - \mathbf{X} \beta) = 0
$$

最后得到$\beta$的估计值：

$$
\hat{\beta} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}
$$

其中$(\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T$也称为$\mathbf{X}$的**伪逆(Moore–Penrose inverse)**。

从矩阵的角度上看$\beta$实际上是对$\mathbf{X}$的列向量进行了线性组合，因此使用最小二乘法的过程也可以理解为将$\mathbf{y}$投影到$\mathbf{X}$列向量构成的空间中得到正交投影$\hat{y} = \mathbf{X} \hat{\beta}$的过程。

<div align=center>
<img src="https://i.imgur.com/Oej54wY.png" width="50%">
</div>

## Polynomial Regression

## Cross Validation

## Reference
- [Chapter 3: Linear Methods for Regression](https://web.stanford.edu/~hastie/ElemStatLearn/printings/ESLII_print12_toc.pdf#page=62)
- [Polynomial Regression](https://en.wikipedia.org/wiki/Polynomial_regression)
- [Cross Validation](https://en.wikipedia.org/wiki/Cross-validation_(statistics))
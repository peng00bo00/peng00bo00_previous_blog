---
layout: article
title: OMSCS-ML课程笔记03-Neural Networks
tags: ["OMSCS", "ML"]
key: OMSCS-ML-03
aside:
  toc: true
sidebar:
  nav: OMSCS-ML
---

> 这个系列是Gatech OMSCS 机器学习课程([CS 7641: Machine Learning](https://omscs.gatech.edu/cs-7641-machine-learning))的同步课程笔记。课程内容涉及监督学习、无监督学习和强化学习三个部分，本节主要介绍监督学习中神经网络的相关内容。
<!--more-->

**神经网络(neural networks)**是一种非常强大的机器学习模型，在分类和回归问题中都有非常多的应用。某种意义上将我们可以把神经网络看做是对生物神经系统的抽象：每个神经元只负责简单的处理和信号收发，将不同的神经元连接起来形成一个网络就可以解决复杂的问题。

神经元作为神经网络中最基本的结构负责对来自其他神经元的信号按权重进行相加，当累积的信号超过阈值时神经元被激活并向它后面的神经元发射一个信号。上述过程可以表示为：

$$
y = f(\sum_{i=1}^n \omega_i x_i - \theta)
$$

<div align=center>
<img src="https://i.imgur.com/9uKWZnV.png" width="90%">
</div>

## Perceptron

最简单的神经网络为**感知机(perceptron)**，此时神经元的阈值为0且激活函数为阶跃函数：

$$
f(x) = 
\left\{
\begin{aligned}
& 1, & & x > 0 \\
& 0, & & \text{otherwise}
\end{aligned}
\right.
$$

<div align=center>
<img src="https://upload.wikimedia.org/wikipedia/commons/d/d9/Dirac_distribution_CDF.svg" width="40%">
</div>

## Gradient Descent

## Sigmoid

## Neural Network Sketch

## Bias

### Restriction Bias

最后我们来讨论神经网络的偏好。

### Preference Bias

## Reference

- Chapter 4: ARTIFICIAL NEURAL NETWORKS, [Machine Learning, Tom Mitchell, McGraw Hill, 1997.](http://www.cs.cmu.edu/afs/cs.cmu.edu/user/mitchell/ftp/mlbook.html)
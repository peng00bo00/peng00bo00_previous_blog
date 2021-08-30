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
y = f(\sum_{i=1}^n \omega_i x_i + b)
$$

<div align=center>
<img src="https://i.imgur.com/9uKWZnV.png" width="90%">
</div>

## Perceptron

最简单的神经网络为**感知机(perceptron)**，此时神经元的阈值为0且对应激活函数为**单位阶跃函数(heaviside step function)**：

$$
f(x) = 
\left\{
\begin{aligned}
& 1, & & x \geq 0 \\
& 0, & & \text{otherwise}
\end{aligned}
\right.
$$

<div align=center>
<img src="https://raw.githubusercontent.com/siebenrock/activation-functions/master/plots/binary_step.png" width="40%">
</div>

感知机可以用来解决二分类问题，而且通过调整神经元的权重单层感知机可以表示所有的基本逻辑运算符包括AND、OR、NOT等。实际上此时感知机的决策边界为二维平面上的直线，只要数据**线性可分(linearly separable)**就一定可以用感知机来描述。相应地，如果数据不是线性可分则不能使用感知机进行描述。一个经典的例子是异或运算XOR：单层感知机无法表示异或运算，需要使用多层感知机才能处理线性不可分的问题。

<div align=center>
<img src="https://i.imgur.com/6XI7z9z.png" width="70%">
</div>

## Training

### Perceptron Learning

对于线性可分的数据，感知机的学习算法如下：

1. 初始化神经元权重$\omega$以及学习率$\eta$；
2. 对数据集进行遍历：
   1. 计算感知机在当前数据上的预测值$\hat{y} = (\omega^T x \geq 0)$；
   2. 如果感知机对当前数据预测正确则继续遍历；
   3. 否则更新参数$\omega \leftarrow \omega + \eta (y - \hat{y}) x$。

感知机的学习算法可以理解为根据数据预测值与实际的误差来调整神经元权重，调整的幅度由学习率$\eta$进行控制。同时可以证明对于线性可分的数据，采用上述的感知机学习算法在有限次迭代后一定可以找到将数据完美划分的超平面。

### Gradient Descent

我们将感知机学习的思想推广到更一般的情况中，就能得到神经网络训练常用的**梯度下降算法(Gradient Descent)**：

1. 初始化神经元权重$\omega$以及学习率$\eta$；
2. 对数据集进行遍历：
   1. 计算神经网络在当前数据上的误差$E$；
   2. 计算误差关于每个权重$\omega_i$的偏导数$\frac{\partial E}{\partial \omega_i}$；
   3. 更新每个参数$\omega_i \leftarrow \omega_i - \eta \frac{\partial E}{\partial \omega_i}$；
   4. 重复以上步骤直至数据集上总误差收敛。

因此对于不同类型的任务只需要选择合适的误差函数并计算相应的偏导数即可。对于大型神经网络显式计算偏导数基本是不现实的，实际中一般是通过**反向传播算法(backpropagation)**从后向前计算每一层的偏导数。同时需要说明的是与感知机学习算法不同，梯度下降算法**不能**保证收敛到全局最优。

## Sigmoid

<div align=center>
<img src="https://raw.githubusercontent.com/siebenrock/activation-functions/master/plots/sigmoid.png" width="40%">
</div>

## Neural Network Sketch

## Bias

### Restriction Bias

最后我们来讨论神经网络的偏好。

### Preference Bias

## Reference

- Chapter 4: ARTIFICIAL NEURAL NETWORKS, [Machine Learning, Tom Mitchell, McGraw Hill, 1997.](http://www.cs.cmu.edu/afs/cs.cmu.edu/user/mitchell/ftp/mlbook.html)
---
layout: article
title: OMSCS-ML课程笔记07-Computational Learning Theory
tags: ["OMSCS", "CS7641-ML"]
key: OMSCS-ML-06
aside:
  toc: true
sidebar:
  nav: OMSCS-ML
---

> 这个系列是Gatech OMSCS 机器学习课程([CS 7641: Machine Learning](https://omscs.gatech.edu/cs-7641-machine-learning))的同步课程笔记。课程内容涉及监督学习、无监督学习和强化学习三个部分，本节主要介绍监督学习中计算学习理论的相关内容。
<!--more-->

## Learning to Learn

到目前为止我们已经介绍了很多类型的机器学习算法，而本节介绍的**计算学习理论(computational learning theory)**不涉及任何具体地算法，而是尝试去解决为什么机器学习是可行的以及我们需要多少样本才能保证学习算法是可靠的这样的问题。

如果将机器学习比作现实生活中的学习过程，那么机器学习算法实际上是使用**自然学习(natural learning)**的模式。在这样的模式下我们只会给学习器提供一系列样本，然后由模型自己来进行学习。我们关心的是需要多少样本才能保证学习器能够学习到正确的假设，称为**样本复杂度(sample complexity)**。

## PAC Learning

计算学习理论的主要成果是**概率近似正确理论(probably approximately correct, PAC)**，基于PAC学习理论我们可以去计算学习算法的样本复杂度。在介绍具体的理论前首先要引入一些相关的概念：假设样本$X$都是从某个分别$D$中采样得到的；$D$可以是任意的分布同时学习器$L$无法得知$D$的信息；学习器$L$的目标是从假设空间$H$中学习到正确的概念$c$。设学习器学习到的假设为$h$，我们定义$h$在分布$D$上的误差为：

$$
error_D(h) = \underset{x \in D}{Pr} [c(x) \neq h(x)]
$$

## VC Dimension

## Reference

- Chapter 7: COMPUTATIONAL LEARNING THEORY, [Machine Learning, Tom Mitchell, McGraw Hill, 1997.](http://www.cs.cmu.edu/afs/cs.cmu.edu/user/mitchell/ftp/mlbook.html)
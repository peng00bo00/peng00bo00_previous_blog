---
layout: article
title: OMSCS-ML课程笔记08-Bayesian Learning and Inference
tags: ["OMSCS", "CS7641-ML"]
key: OMSCS-ML-08
aside:
  toc: true
sidebar:
  nav: OMSCS-ML
---

> 这个系列是Gatech OMSCS 机器学习课程([CS 7641: Machine Learning](https://omscs.gatech.edu/cs-7641-machine-learning))的同步课程笔记。课程内容涉及监督学习、无监督学习和强化学习三个部分，本节主要介绍监督学习中贝叶斯学习理论的相关内容。
<!--more-->

## Bayesian Learning

### Bayes' Theorem

在正式介绍贝叶斯学习前首先来回顾一下**贝叶斯定理(Bayes theorem)**。对任意事件$A$和$B$，事件$A$在已知事件$B$发生的条件下的条件概率为：

$$
P(A \vert B) = \frac{P(A, B)}{P(B)} = \frac{P(B \vert A) P(A)}{P(B)} = \frac{P(B \vert A) P(A)}{\sum_A P(B \vert A) P(A)}
$$

其中条件概率$P(A \vert B)$也被称为**后验概率(posterior probability)**；单个随机变量的概率$P(A)$和$P(B)$称为**先验概率(prior probability)**；条件概率$P(B \vert A)$称为**似然(likelihood)**。

### MAP and MLE

在贝叶斯学习理论中我们取事件$A$为待求假设$h$，事件$B$为已知数据$D$，那么在已知训练数据的条件下待求假设$h$的概率可以表示为：

$$
P(h \vert D) = \frac{P(D \vert h) P(h)}{P(D)} \sim P(D \vert h) P(h)
$$

显然我们希望求解得到的假设$h$为在已知数据情况下概率最大的假设，称之为**最大后验假设(maximum a posteriori hypothesis)**：

$$
h_{MAP} = \underset{h \in H}{\arg \max} P(D \vert h) P(h)
$$

上式说明后验概率取决于假设$h$生成数据集$D$的似然$P(D \vert h)$以及假设自身的先验概率$P(h)$。如果我们假设$h$服从均匀分布则可以省略掉先验项$P(h)$，此时计算得到的假设称为**最大似然假设(maximum likelihood hypothesis)**：

$$
h_{ML} = \underset{h \in H}{\arg \max} P(D \vert h)
$$

因此贝叶斯学习的基本框架是首先根据domain knowledge来设置先验$P(h)$，然后计算后验概率$P(h \vert D)$并选择其中具有最大后验的假设。不过需要说明的是在大多数情况下显式计算后验概率是不现实的(intractable)。

### Least-Squared Error Hypothesis

尽管在很多时候我们无法显式计算后验概率，但我们仍然可以利用贝叶斯法则来理解很多问题。以回归问题为例，假设存在一个函数$h$将自变量$x$映射到$y$，由于噪声$e$的存在我们观测到的结果实际上是带噪声的数据：

$$
d_i = h(x_i) + e_i
$$

其中噪声$e$与自变量$x$相互独立，且服从正态分布$e \sim N(0, \sigma^2)$。噪声的加法模型说明训练数据$(x_i, d_i)$来自于正态分布$d_i \sim N(h(x_i), \sigma^2)$，每个样本的概率为：

$$
p = \frac{1}{\sqrt{2 \pi} \sigma} \exp \bigg\{ -\frac{(d_i - h(x_i))^2}{2 \sigma^2} \bigg\}
$$

由于样本是独立同分布的，似然函数为它们概率的乘积：

$$
P(D \vert h) = \prod_i \frac{1}{\sqrt{2 \pi} \sigma} \exp \bigg\{ -\frac{(d_i - h(x_i))^2}{2 \sigma^2} \bigg\} \sim \prod_i \exp \bigg\{ -\frac{(d_i - h(x_i))^2}{2 \sigma^2} \bigg\}
$$

通过取对数得到累加的形式：

$$
\ln P(D \vert h) \sim -\sum_i (d_i - h(x_i))^2
$$

如果我们假设$h$服从均匀分布，可以得到极大似然估计：

$$
\begin{aligned}
h_{ML} &= \underset{h \in H}{\arg \max} P(D \vert h) \\
&= \underset{h \in H}{\arg \max} \ln P(D \vert h) \\
&= \underset{h \in H}{\arg \max} -\sum_i (d_i - h(x_i))^2 \\
&= \underset{h \in H}{\arg \min} \sum_i (d_i - h(x_i))^2
\end{aligned}
$$

与最小二乘法的优化目标相同。上式说明贝叶斯视角下的最小二乘法实际上就是对高斯噪声下的数据进行极大似然估计。

### Minimum Description Length Principle

先验$P(h)$对于计算最大后验假设会产生重大的影响，通过取对数可以将最大后验估计表示为：

$$
\begin{aligned}
h_{MAP} &= \underset{h \in H}{\arg \max} P(D \vert h) P(h) \\
&= \underset{h \in H}{\arg \max} \log_2 P(D \vert h) + \log_2 P(h) \\
&= \underset{h \in H}{\arg \min} -\log_2 P(D \vert h) - \log_2 P(h)
\end{aligned}
$$

从信息论的角度上看对任意随机事件$x$进行编码所需的最小字节数为$- \log_2 P(x)$，因此最大后验也可以认为是选择最小编码长度的假设：似然项$-\log_2 P(D \vert h)$表示给定假设$h$对数据集$D$进行编码所需的长度，$h$生成数据集$D$的概率越大所需字节数越小；而先验项$-\log_2 P(h)$则表示假设$h$自身的复杂度，$h$越简单它出现的概率越高对它进行编码所需的字节数也越小。这说明最大后验估计会倾向于选择更为简单的假设，从而防止出现过拟合的问题。

### Bayesian Classification

贝叶斯学习理论除了可以选择假设还可以对新的数据进行预测。假设在数据集$D$外有一个来自同样分布的数据$v$，利用贝叶斯公式可以计算后验概率：

$$
P(v \vert D) = \sum_{h \in H} P(v, h \vert D) = \sum_{h \in H} P(v \vert D, h) P(h \vert D) = \sum_{h \in H} P(v \vert h) P(h \vert D)
$$

上式说明数据$v$在已知数据集$D$情况下的后验概率等于假设空间中每个假设$h$产生$v$概率的加权求和，每个假设$h$的权重等于它在数据集上的后验概率。

对于分类问题可以令$v$表示新样本对应的类别，此时的最大后验估计为：

$$
\underset{v \in V}{\arg \max} \sum_{h \in H} P(v \vert h) P(h \vert D)
$$

满足上式的分类器称为**贝叶斯最优分类器(Bayes optimal classifier)**，它是在相同假设空间和先验条件下的最优分类器。同时贝叶斯最优分类器的输出等于假设空间中每个假设输出的加权求和，对应的权重是相应假设的后验概率。

## Bayesian Inference

## Reference

- Chapter 6: BAYESIAN LEARNING, [Machine Learning, Tom Mitchell, McGraw Hill, 1997.](http://www.cs.cmu.edu/afs/cs.cmu.edu/user/mitchell/ftp/mlbook.html)
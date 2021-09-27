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
h_{MAP} = \argmax_{h \in H} P(D \vert h) P(h)
$$

上式说明后验概率取决于假设$h$生成数据集$D$的似然$P(D \vert h)$以及假设自身的先验概率$P(h)$。如果我们假设$h$服从均匀分布则可以将先验项$P(h)$省略掉，此时获得的假设称为**最大似然假设(maximum likelihood hypothesis)**：

$$
h_{ML} = \argmax_{h \in H} P(D \vert h)
$$

### Bayesian Classification

## Bayesian Inference
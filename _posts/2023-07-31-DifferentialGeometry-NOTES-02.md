---
layout: article
title: 微分几何笔记02-曲线论
tags: ["CG", "Geometry Processing", "Math"]
key: DifferentialGeometry-02
aside:
  toc: true
sidebar:
  nav: DifferentialGeometry
---

> 这个系列是北京大学陈维桓教授《微分几何(第二版)》的学习笔记，主要涉及古典微分几何中曲线曲面理论的相关知识。系统学习微分几何对于理解计算机图形学中的各种几何处理算法是十分有益的。
<!--more-->

## 正则参数曲线

### 参数曲线

首先我们来介绍**曲线**的概念。在微分几何中我们认为$$\mathbb{E}^3$$中的曲线$$C$$是从区间$$[a, b]$$到$$\mathbb{E}^3$$的一个连续映射，记为

$$
p: [a, b] \rightarrow \mathbb{E}^3
$$

称为**参数曲线**。给定$$\mathbb{E}^3$$中的正交标架$$\{O; \boldsymbol{i}, \boldsymbol{j}, \boldsymbol{k} \}$$，则曲线$$C$$上的点$$p(t)$$等同于向量$$\overrightarrow{Op(t)}$$。令$$\boldsymbol{r}(t) = \overrightarrow{Op(t)}$$，则$$\boldsymbol{r}(t)$$可以表示为向量函数

$$
\boldsymbol{r}(t) = x(t) \ \boldsymbol{i} + y(t) \ \boldsymbol{j} + z(t) \ \boldsymbol{k}, \ \ t \in [a, b]
$$

记为

$$
\boldsymbol{r}(t) = (x(t), y(t), z(t)), \ \ t \in [a, b]
$$

其中$$t$$是曲线的参数，上式称为曲线$$C$$的**参数方程**。

### 曲线的切线

根据导数定义可知

$$
\boldsymbol{r}'(t) = \lim_{\Delta t \to 0} \frac{\boldsymbol{r}(t + \Delta t) - \boldsymbol{r}(t)}{\Delta t} = (x'(t), y'(t), z'(t))
$$

如果坐标函数$$x'(t)$$，$$y'(t)$$，$$z'(t)$$是连续可微的，则称曲线$$\boldsymbol{r}(t)$$是连续可微的。这个概念与笛卡尔坐标系的选取无关。

导数$$\boldsymbol{r}'(t)$$有明显的几何意义。$$\boldsymbol{r}(t + \Delta t) - \boldsymbol{r}(t)$$表示点$$\boldsymbol{r}(t)$$到点$$\boldsymbol{r}(t + \Delta t)$$的有向线段，因此$$\frac{\boldsymbol{r}(t + \Delta t) - \boldsymbol{r}(t)}{\Delta t}$$表示经过点$$\boldsymbol{r}(t)$$和点$$\boldsymbol{r}(t + \Delta t)$$的割线$$l$$方向向量。当$$\Delta t \to 0$$时，割线$$l$$的极限位置就是曲线在点$$\boldsymbol{r}(t)$$处的**切线**。如果$$\boldsymbol{r}'(t) \neq \boldsymbol{0}$$，则$$\boldsymbol{r}'(t)$$是曲线在点$$\boldsymbol{r}(t)$$处的切线的方向向量，称为曲线的**切向量**如下图所示。

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/zIFDBhi.png" width="80%">
</div>

此时曲线在点$$\boldsymbol{r}(t)$$处的切线是可以完全确定的，这样的点称为曲线的**正则点**。而曲线在正则点处的切线方程为

$$
\boldsymbol{X}(u) = \boldsymbol{r}(t) + u \boldsymbol{r}'(t)
$$

其中$$t$$是固定的，$$u$$是切线上点的参数，$$\boldsymbol{X}(u)$$是从原点$$O$$指向切线上参数为$$u$$的点的有向线段。

### 正则参数曲线

我们称参数曲线$$\boldsymbol{r}(t)$$为**正则参数曲线**当且仅当它满足以下两个条件：

(1) $$\boldsymbol{r}(t)$$至少是自变量$$t$$的三次以上连续可微函数 *(曲线的几何不变量涉及$$\boldsymbol{r}(t)$$的三次导数)*

(2) 处处是正则点，即对任意的$$t$$有$$\boldsymbol{r}'(t) \neq \boldsymbol{0}$$

我们把参数$$t$$增大的方向称为该参数曲线的正向，因此$$\boldsymbol{r}'(t)$$正好指向曲线的正向。

### 参数变换

显然曲线参数方程的表达式与坐标系的选取有关，另外在固定的笛卡尔直角坐标系下还可以对参数进行一些变换。为了保证正则参数曲线的两个条件在参数变换下保持不变，我们要求参数变换$$t = t(u)$$需要满足以下两个条件：

(1) $$t(u)$$是$$u$$的三次以上连续可微函数

(2) $$t'(u)$$处处不为$$0$$

这样在参数变换$$t = t(u)$$下，曲线的参数方程可以表示为$$\boldsymbol{r} (t(u))$$，简记为$$\boldsymbol{r}(u)$$。根据求导的链式法则有

$$
\boldsymbol{r}'(u) = \frac{d}{d u} \boldsymbol{r}(t(u)) = \boldsymbol{r}'(t(u)) \cdot t'(u)
$$

## 曲线的弧长
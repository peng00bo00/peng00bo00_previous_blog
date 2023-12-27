---
layout: article
title: 微分几何笔记05-曲面论基本定理
tags: ["CG", "Geometry Processing", "Math", "Differential Geometry"]
key: DifferentialGeometry-05
aside:
  toc: true
sidebar:
  nav: DifferentialGeometry
---

> 这个系列是北京大学陈维桓教授《微分几何(第二版)》的学习笔记，主要涉及古典微分几何中曲线曲面理论的相关知识。系统学习微分几何对于理解计算机图形学中的各种几何处理算法是十分有益的。本节介绍曲面论基本定理。
<!--more-->

## 自然标架的运动公式

在研究空间曲线时，我们在曲线上曲率不为零的每一个点处附加了一个确定的[Frenet标架](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的曲率和frenet标架)，那么Frenet标架沿曲线运动的状况便反映出曲线本身的弯曲情况。Frenet标架可以通过曲线的参数方程的导数和适当的代数运算显式地表示出来，从而$$\mathbb{E}$$中一条曲线可以转化为$$\mathbb{E}$$上所有的标架构成的空间中的一条曲线。曲线论的基本定理和存在定理都是通过标架空间中的这个单参数标架族进行证明的，因为只有这个单参数标架族在运动时给出的信息才完整地表达曲线的弯曲形状。对于空间中的正则参数曲面$$\boldsymbol{r} = \boldsymbol{r} (u, v)$$，），我们也需要以某种确定的方式在每一点附加一个标架，这个标架就是自然标架$$\{ \boldsymbol{r}; \boldsymbol{r}_u, \boldsymbol{r}_v, \boldsymbol{n} \}$$。与曲线的情形不同的是，自然标架和曲面的参数选择是有关系的，而且一般来说自然标架不是正交标架，更不是单位正交标架。当然，我们可以在曲面上取单位正交标架场，如$$\{ \boldsymbol{r}; \boldsymbol{e}_1, \boldsymbol{e}_2, \boldsymbol{n} \}$$｝，其中$$\boldsymbol{e}_1$$, $$\boldsymbol{e}_1$$是曲面在该点的彼此正交的主方向单位向量。但是，主方向本身并不能够像曲线的Frenet标架那样从曲面的参数方程$$\boldsymbol{r} = \boldsymbol{r}(u, v)$$的偏导数直截了当地显式表示出来。即使我们假定在曲面上取了正交曲率线网作为曲面的参数曲线网，也只能做到$$\boldsymbol{r}_u \parallel \boldsymbol{e}_1$$，$$\boldsymbol{r}_v \parallel \boldsymbol{e}_2$$，而不是$$\boldsymbol{r}_u = \boldsymbol{e}_1$$，$$\boldsymbol{r}_v = \boldsymbol{e}_2$$。由此可见，从自然标架场出发展开我们的理论比较方便。后来Cartan发展了活动标架理论来研究微分几何学，在曲面上可以取任意的标架场，包括单位正交标架场，此时要用"微分"替代"偏导数"，因而相应地要用到外微分方法。我们将在后面介绍Cartan的活动标架和外微分法。

### Einstein求和约定

### Christoffel记号

## 曲面的唯一性定理

## 曲面论基本方程

## 曲面的存在性定理

## Gauss定理
---
layout: article
title: 微分几何笔记06-测地曲率和测地线
tags: ["CG", "Geometry Processing", "Math", "Differential Geometry"]
key: DifferentialGeometry-06
aside:
  toc: true
sidebar:
  nav: DifferentialGeometry
---

> 这个系列是北京大学陈维桓教授《微分几何(第二版)》的学习笔记，主要涉及古典微分几何中曲线曲面理论的相关知识。系统学习微分几何对于理解计算机图形学中的各种几何处理算法是十分有益的。本节介绍内蕴几何学中测地曲率和测地线的相关内容。
<!--more-->

由Gauss开创的曲面内蕴几何学有丰富的内容。本章的重点是研究曲面上曲线的测地曲率和测地线，在研究它们的外在特征和性质的同时，更主要的是证明它们可以通过曲面的第一基本形式进行计算，而与曲面的第二基本形式无关。因此它们在曲面的保长对应下是保持不变的，是曲面的内蕴性质。通过本章的学习，使我们了解曲面内蕴几何学的主要研究对象是什么，从而为今后学习黎曼几何学打下基础。

## 测地曲率和测地挠率

设正则参数曲面$$S$$的方程是$$\boldsymbol{r} = \boldsymbol{r}(u^1, u^2)$$，$$C$$是曲面$$S$$上的一条曲线，它的方程是$$u^\alpha = u^\alpha (s)$$，$$\alpha = 1, 2$$，其中$$s$$是曲线$$C$$的弧长参数。那么$$C$$作为空间$$\mathbb{E}^3$$中曲线的参数方程是

$$
\boldsymbol{r} = \boldsymbol{r} (s) = \boldsymbol{r} (u^1 (s), u^2 (s))
$$

在[曲线论](/2023/07/31/DifferentialGeometry-NOTES-02.html#曲线的曲率和frenet标架)中我们曾经沿空间曲线$$C$$建立了Frenet标架$$\{ \boldsymbol{r} (s); \boldsymbol{\alpha} (s), \boldsymbol{\beta} (s), \boldsymbol{\gamma}(s) \}$$。但是，曲线$$C$$的Frenet标架场没有考虑到目前的曲线$$C$$落在曲面$$S$$上的事实，因此Frenet标架及其运动公式(Frenet公式)自然不会反映曲线$$C$$和曲面$$S$$之间相互约束的关系。现在，我们要沿曲线$$C$$建立一个新的正交标架场$$\{ \boldsymbol{r}; \boldsymbol{e}_1, \boldsymbol{e}_2, \boldsymbol{e}_3 \}$$，使得它兼顾曲线$$C$$和曲面$$S$$，其定义是
$$
\begin{aligned}
\boldsymbol{e}_1 &= \frac{\mathrm{d} \boldsymbol{r} (s)}{\mathrm{d} s} = \boldsymbol{\alpha} (s) \\
\boldsymbol{e}_3 &= \boldsymbol{n} (s) \\
\boldsymbol{e}_2 &= \boldsymbol{e}_3 \times \boldsymbol{e}_1 = \boldsymbol{n} (s) \times \boldsymbol{\alpha} (s) \\
\end{aligned}
$$

<div align=center>
<img src="https://search.pstatic.net/common?src=https://i.imgur.com/DjV5ATz.png" width="80%">
</div>

直观上，向量$$\boldsymbol{e}_2$$是将曲线$$C$$的切向量$$\boldsymbol{e}_1 = \boldsymbol{\alpha}$$围绕曲面$$S$$的单位法向量$$\boldsymbol{n}$$按正向旋转90°得到的。与[存在对应关系的曲线偶](/2023/07/31/DifferentialGeometry-NOTES-02.html#存在对应关系的曲线偶)相对照不难发现，我们在这里对于曲面$$S$$上的曲线$$C$$建立正交标架场的做法和平面曲线建立正交标架场的做法是一致的。换言之我们现在的目标是把平面上的曲线论推广成为曲面$$S$$上的曲线论。

## 测地线

## 测地坐标系和法坐标系

## 常曲率曲面

## 曲面上切向量的平行移动

## 抽象曲面

## 抽象曲面上的几何学

## 抽象曲面的曲率

## Gauss-Bonnet公式
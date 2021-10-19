---
layout: article
title: OMSCS-CV课程笔记11-Tracking
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-11
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍目标跟踪的相关内容。
<!--more-->

## Introduction to Tracking

**目标跟踪(tracking)**是视频处理和分析的基本内容之一，我们希望能对视频中的物体运动进行跟踪，从而得到它的运动轨迹。目标跟踪的主要难点如下：

1. 在很多场景中无法计算光流；
2. 当物体运动很快时会产生比较大的位移；
3. 观测的误差容易发生累计；
4. 物体运动过程中存在遮挡的情况。

为了处理这些问题，一个基本的思路是考虑物体的**动力学模型(dynamic model)**。这样当物体发生运动时利用动力学模型可以对它可能出现的位置进行预测，从而缩小搜索范围并降低观测误差。在这种情况下目标跟踪和逐帧的检测是有一定差别的：目标检测是在每一帧图像上独立地进行检测(红色框)，相邻图像之间没有任何联系；而跟踪则需要根据动力学模型在前一帧的基础上估计物体的当前位置，然后结合当前帧的观测结果进行更新从而确定物体的实际位置(蓝色框)。

<div align=center>
<img src="https://i.imgur.com/GDDsNlQ.png" width="90%">
</div>

<div align=center>
<img src="https://i.imgur.com/lW0cqpC.png" width="90%">
</div>

因此，目标跟踪的目标是利用动力学模型来缩减搜索空间并结合观测结果来减小误差，进而得到光滑的物体运动轨迹。为了便于讨论我们这里对目标跟踪的场景进行一些限制：

1. 物体不会在场景中突然消失或是突然出现；
2. 相机的位置和姿态不会发生突变；
3. 物体和场景只会发生缓慢的运动。

## Parametric Models

### Tracking as Inference

### The Kalman Filter

## Non-Parametric Models

## Reference
---
layout: article
title: OMSCS-CV课程笔记06-Camera Calibration
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-06
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍相机标定的相关内容。
<!--more-->

## Geometric Camera Calibration

在[Camera Models](/2021/09/07/OMSCS-CV-NOTES-04.html#modeling-projection)一节中我们介绍了齐次坐标和相机的投影模型，从而将三维空间中的点投影到图像平面上。本节课中我们会把这个方法推广到更一般的情形中：我们不再假定坐标原点位于相机的投影中心，而是将任意坐标系下的点投影到图像平面上。我们把确定空间坐标与图像坐标之间关系的过程称为**相机的几何标定(geometric camera calibration)**。

相机标定包括2部分内容：

1. 世界坐标到相机坐标的变换，这部分称为相机的**外参数(extrinisic parameters)**或**位姿(pose)**。
2. 相机坐标到图像坐标的变换，这部分称为相机的**内参数(intrinisic parameters)**。

## Extrinsic Camera Calibration

### Translation

### Rotation

### Rigid Transformations

## Instrinsic Camera Calibration

## Calibrating Cameras
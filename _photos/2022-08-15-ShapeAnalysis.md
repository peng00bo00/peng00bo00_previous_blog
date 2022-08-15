---
layout: article
title: Shape Analysis Homeworks
key: gallery
cover: https://i.imgur.com/KrAIIuX.gif
aside:
  toc: true
---

> Homeworks in [MIT 6.838: Shape Analysis](https://groups.csail.mit.edu/gdpgroup/6838_spring_2021.html).
<!--more-->

## Homework 1: Discrete and Smooth Curves

### Discrete Curvature of a Plane Curve

#### Gradient $\nabla_{\mathbf{x}_i} s$

$$
\nabla_{\mathbf{x}_i} s =\frac{\mathbf{x}_i - \mathbf{x}_{i-1}}{\Vert \mathbf{x}_i - \mathbf{x}_{i-1} \Vert_2} + \frac{\mathbf{x}_i - \mathbf{x}_{i+1}}{\Vert \mathbf{x}_i - \mathbf{x}_{i+1} \Vert_2}
$$

<div align=center>
<img src="https://i.imgur.com/HEp18iQ.png" width="50%">
</div>

#### Discrete Curvature

$$
\kappa = 2 \sin \frac{\theta}{2}
$$

<div align=center>
<img src="https://i.imgur.com/YMaEmwy.png" width="51%">
</div>

#### Curve Shortening Flow

$$
\mathbf{x}_i' = \mathbf{x}_i - (\nabla_{\mathbf{x}_i} s) h
$$

<div align=center>
<img src="https://i.imgur.com/J1jChfg.gif" width="50%">
</div>

<div align=center>
<img src="https://i.imgur.com/lE8Rv1s.gif" width="50%">
</div>

<div align=center>
<img src="https://i.imgur.com/KE61wET.gif" width="50%">
</div>

### Discrete Elastic Rods

<div align=center>
<img src="https://i.imgur.com/cHm2IwG.gif" width="45%">
<img src="https://i.imgur.com/VvSJcuN.gif" width="45%">
<img src="https://i.imgur.com/HLOl1tB.gif" width="45%">
<img src="https://i.imgur.com/KrAIIuX.gif" width="45%">
</div>
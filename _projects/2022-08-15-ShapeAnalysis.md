---
layout: article
title: Shape Analysis Homeworks
key: gallery
cover: https://pic1.xuehuaimg.com/proxy/i.imgur.com/KrAIIuX.gif
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
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/HEp18iQ.png" width="50%">
</div>

#### Discrete Curvature

$$
\kappa = 2 \sin \frac{\theta}{2}
$$

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/YMaEmwy.png" width="51%">
</div>

#### Curve Shortening Flow

$$
\mathbf{x}_i' = \mathbf{x}_i - (\nabla_{\mathbf{x}_i} s) h
$$

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/J1jChfg.gif" width="50%">
</div>

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/lE8Rv1s.gif" width="50%">
</div>

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/KE61wET.gif" width="50%">
</div>

### Discrete Elastic Rods

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/cHm2IwG.gif" width="45%">
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/VvSJcuN.gif" width="45%">
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/HLOl1tB.gif" width="45%">
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/KrAIIuX.gif" width="45%">
</div>

## Homework 2: Surfaces and Curvature

### Mean Curvature Flow with Explicit Integrator

$$
\frac{\mathbf{p} (t+\tau) - \mathbf{p} (t)}{\tau} = - \mathbf{M}^{-1} (\mathbf{p} (t)) \cdot \mathbf{L} (\mathbf{p} (t)) \cdot \mathbf{p} (t)
$$

$$
\mathbf{p} (t+\tau) = \mathbf{p} (t) - \tau \mathbf{M}^{-1} (\mathbf{p} (t)) \cdot \mathbf{L} (\mathbf{p} (t)) \cdot \mathbf{p} (t)
$$

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/14jPnsN.gif" width="50%">
</div>

### Mean Curvature Flow with (Semi-)Implicit Integrator

$$
\frac{\mathbf{p} (t+\tau) - \mathbf{p} (t)}{\tau} = - \mathbf{M}^{-1} (\mathbf{p} (t)) \cdot \mathbf{L} (\mathbf{p} (t)) \cdot \mathbf{p} (t+\tau)
$$

$$
\mathbf{p} (t+\tau) =\bigg(\mathbf{I} + \tau \mathbf{M}^{-1} (\mathbf{p} (t)) \cdot \mathbf{L} (\mathbf{p} (t)) \bigg)^{-1} \cdot \mathbf{p} (t) 
$$

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/Bl0zqwZ.gif" width="50%">
</div>

### Non-Singular Mean Curvature Flow

$$
\mathbf{p} (t+\tau) = \bigg(\mathbf{I} + \tau \mathbf{M}^{-1} (\mathbf{p} (t)) \cdot \mathbf{L} (\mathbf{p} (0)) \bigg)^{-1} \cdot \mathbf{p} (t) 
$$

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/RDqlDh7.gif" width="50%">
</div>

## Homework 3: Geodesics, Distance, and Metric Embedding

### Swiss-Roll DataSet

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/KiBi29n.png" width="45%">
</div>

### Maximum Variance Unfolding

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/s4WDk8X.png" width="45%">
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/eyU9fFs.png" width="45%">
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/EwffIl4.png" width="45%">
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/1FDabII.png" width="45%">
</div>

## Homework 4: Laplacian and Vector Fields

### Helmholtz Decomposition

1. $$\nabla \cdot V = \nabla \cdot \nabla \zeta = \Delta \zeta$$
2. $$\nabla \times W = V - \nabla \zeta$$

### Geodesic Distance from the Laplacian

#### Heat Kernel & Normalized Gradient

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/92t2TcB.png" width="50%">
</div>

#### Divergences

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/U3vhQx3.png" width="50%">
</div>

#### Geodesic Distances

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/JhFYXjq.png" width="50%">
</div>

### Parallel Transport from the Connection Laplacian

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/GQYwCBz.png" width="50%">
</div>

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/k5hiqoa.png" width="50%">
</div>

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/DCl9ppI.png" width="50%">
</div>

### Operator Approach to Tangent Vector Fields

#### Scalar Field Advection

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/obuaX0R.gif" width="50%">
</div>

## Manifold Optimization and Optimal Transport

### Optimal Transport

1. $W(\mathbf{p}, \mathbf{q})$ measures the minimum cost of transporting $\mathbf{p}$ to $\mathbf{q}$.

2. Let $K_\alpha = e^{1-\frac{C}{\alpha}}$, then

$$
\begin{aligned}
\alpha \cdot \text{KL} (T \Vert K_\alpha) &= \alpha \cdot \sum_{ij} T_{ij} \ln{\frac{T_{ij}}{(K_\alpha)_{ij}}} = \alpha \cdot \bigg( \sum_{ij} T_{ij} \ln{T_{ij}} - \sum_{ij} T_{ij} \ln{(K_\alpha)_{ij}} \bigg) \\
&= \alpha \cdot \sum_{ij} T_{ij} \ln{T_{ij}} + \alpha \cdot \sum_{ij} T_{ij} \cdot \bigg( \frac{C_{ij}}{\alpha}-1 \bigg) \\
&= \sum_{ij} T_{ij} \cdot C_{ij} + \alpha \cdot \bigg( \sum_{ij} T_{ij} \ln{T_{ij}} - 1 \bigg)
\end{aligned}
$$

3. 

  The Lagrange could be expressed as:

$$
\mathcal{L} (T; \lambda, \mu) = \sum_{ij} T_{ij} \cdot C_{ij} + \alpha \cdot \bigg( \sum_{ij} T_{ij} \ln{T_{ij}} - 1 \bigg) + \sum_i \lambda_i \cdot \bigg( \sum_j T_{ij} - p_i \bigg) + \sum_j \mu_j \cdot \bigg( \sum_i T_{ij} - q_j \bigg)
$$

  where $\lambda_i$ and $\mu_j$ are Lagrange multipliers.
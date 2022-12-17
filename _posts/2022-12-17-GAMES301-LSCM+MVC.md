---
layout: article
title: LSCM + Mean Value Coordinates 论文笔记
tags: ["CG", "GAMES301", "Geometry Processing"]
key: GAMES301-17
aside:
  toc: true
sidebar:
  nav: GAMES301
---

> GAMES301-曲面参数化([GAMES 301: Surface Parameterization](http://staff.ustc.edu.cn/~renjiec/GAMES301/index.html))作业3解析与matlab实现。
<!--more-->

## LSCM

**LSCM(least squares conformal map)**是经典的共形参数化方法。我们在课程中介绍过共形映射需要满足[Cauchy-Riemann方程](/2022/11/11/GAMES301-NOTES-10.html#plane-to-plane)：

$$
\begin{cases}
\frac{\partial f_x}{\partial x} = \frac{\partial f_y}{\partial y} \\
\frac{\partial f_x}{\partial y} =-\frac{\partial f_y}{\partial x} \\
\end{cases}
\Leftrightarrow
J = 
\begin{bmatrix}
a & -b \\
b & a
\end{bmatrix}
$$

从Jacobian矩阵来看，Cauchy-Riemann方程说明映射$f$是一个相似变换(旋转+缩放)因此不会改变向量的夹角。对于大多数网格我们可能很难保证映射严格满足Cauchy-Riemann方程，此时可以构造一个共形能量来描述映射$f$违背共形映射的程度，而LSCM的原理就是通过最小化共形能量来建立所需的共形映射。

<div align=center>
<img src="https://i.imgur.com/EHNaGWb.png" width="80%">
</div>

### Conformality in a Triangulation

LSCM使用了复平面来推导共形能量。设三角形$T$在其局部坐标系下的初始构型为$$\{ (x_1, y_1), (x_2, y_2), (x_3, y_3) \}$$，在复平面上二维向量可以直接转换为复数：

$$
\{ x_i + i \ y_i \vert i = 1,2,3 \}
$$

类似地，我们把参数化后uv平面上的坐标也表示为复数形式：

$$
\{ u_i + i \ v_i \vert i = 1,2,3 \}
$$

使用复数形式的好处在于我们可以把坐标转换为标量函数进行推导。假设映射$\mathcal{X}: \mathbb{C} \mapsto \mathbb{C}$将参数平面嵌入到三角形局部坐标系中，当$\mathcal{X}$为共形映射时需要满足复数形式的Cauchy-Riemann方程：

$$
\frac{\partial \mathcal{X}}{\partial u} - i \frac{\partial \mathcal{X}}{\partial v} = 0
$$

利用反函数导数定理可以得到$\mathcal{X}$的反函数$\mathcal{U} = u + i \ v$需要满足：

$$
\frac{\partial \mathcal{U}}{\partial x} + i \frac{\partial \mathcal{U}}{\partial y} = 0
$$

接下来我们定义共形能量$C$为等式左端的平方在整个三角形上的积分：

$$
C(T) = \int_T \bigg\vert \frac{\partial \mathcal{U}}{\partial x} + i \frac{\partial \mathcal{U}}{\partial y} \bigg\vert^2 \ dA
$$

显然当$\mathcal{U}$为共形映射时$C(T)$为0，否则三角形上会产生共形能量。对网格上每个三角形进行求和就得到了网格的共形能量：

$$
C(\mathcal{T}) = \sum_i C(T_i)
$$

### Gradient in a Triangle

对于线性三角形网格，其共形能量在三角形内每一点都是相同的。因此我们可以把积分转换为能量与三角形面积相乘：

$$
C(T) = \int_T \bigg\vert \frac{\partial \mathcal{U}}{\partial x} + i \frac{\partial \mathcal{U}}{\partial y} \bigg\vert^2 \ dA = \bigg\vert \frac{\partial \mathcal{U}}{\partial x} + i \frac{\partial \mathcal{U}}{\partial y} \bigg\vert^2 A_T
$$

上式说明我们只需要计算三角形面积$A_T$以及内部的共形能量即可。对于三角形顶点上定义的标量函数$u(x, y)$，其梯度在三角形内部有解析形式：

$$
\begin{bmatrix}
\frac{\partial u}{\partial x} \\ \frac{\partial u}{\partial y}
\end{bmatrix}
=
\frac{1}{2 A_T}
\begin{bmatrix}
y_2-y_3 & y_3-y_1 & y_1-y_2 \\
x_3-x_2 & x_1-x_3 & x_2-x_1 \\
\end{bmatrix}
\begin{bmatrix}
u_1 \\ u_2 \\ u_2
\end{bmatrix}
$$

其中$u_1, u_2, u_3$分别为顶点上的函数值。对于复函数$\mathcal{U}$我们可以整理得到：

$$
\frac{\partial \mathcal{U}}{\partial x} + i \frac{\partial \mathcal{U}}{\partial y} 
=
\frac{i}{2 A_T}
\begin{bmatrix}
W_1 & W_2 & W_3
\end{bmatrix}
\begin{bmatrix}
U_1 \\ U_2 \\ U_3
\end{bmatrix}
$$

其中

$$
\begin{cases}
W_1 = (x_3 - x_2) + i \ (y_3 - y_2) \\
W_2 = (x_1 - x_3) + i \ (y_1 - y_3) \\
W_3 = (x_2 - x_1) + i \ (y_2 - y_1) \\
\end{cases}
\ \ \ 
\begin{cases}
U_1 = u_1 + i \ v_1 \\
U_2 = u_2 + i \ v_2 \\
U_3 = u_3 + i \ v_3 \\
\end{cases}
$$

这样整个三角形上的共形能量可以表示为：

$$
\begin{aligned}
C(T) &= \bigg\vert \frac{\partial \mathcal{U}}{\partial x} + i \frac{\partial \mathcal{U}}{\partial y} \bigg\vert^2 A_T \\
&= \frac{1}{4 A_T} 
\bigg\Vert 
\begin{bmatrix}
W_1 & W_2 & W_3
\end{bmatrix}
\begin{bmatrix}
U_1 & U_2 & U_3
\end{bmatrix}^T
\bigg\Vert^2 \\
&\propto 
\frac{1}{A_T} 
\bigg\Vert 
\begin{bmatrix}
W_1 & W_2 & W_3
\end{bmatrix}
\begin{bmatrix}
U_1 & U_2 & U_3
\end{bmatrix}^T
\bigg\Vert^2 \\
\end{aligned}
$$

对所有三角形求和后就得到了网格上的共形能量，其可以表示为关于顶点复函数的二次型：

$$
C(\mathcal{T}) = \mathbf{U}^* \mathcal{C} \mathbf{U}
$$

上标$^*$表示共轭转置。二次型的系数矩阵$\mathcal{C}$可以分解为：

$$
\mathcal{C} = \mathcal{M}^* \mathcal{M}
$$

$$
\mathcal{M}_{ij} = 
\begin{cases}
\frac{W_{j, T_i}}{\sqrt{A_{T_i}}} & \text{if vertex j belongs to triangle i} \\
0, & \text{otherwise}
\end{cases}
$$

### Least Square Optimization

```matlab
function As = doubleArea(V, F)
%% Compute doubled area of triangles
%% Args:
%%      V[nV, 3]: vertices in 3D
%%      F[nF, 3]: face connectivity
%% Returns:
%%      As[nF, 1]: doubled area of triangles

nF = size(F, 1);

Es = reshape(V(F(:, 2:3), :)-V(F(:, [1 1]), :), [nF 2 3]);
As = vecnorm(cross(Es(:,1,:), Es(:, 2, :), 3), 2, 3);

end
```

```matlab
function uv = LSCM(V, F)
%% LSCM parameterization
%% Args:
%%      V[nV, 3]: vertices in 3D
%%      F[nF, 3]: face connectivity
%% Returns:
%%      uv[nV, 2]: uv coordinates

nV = size(V, 1);
nF = size(F, 1);

%% areas
AT = doubleArea(V, F);
AT_sq = sqrt(AT);

%% rest pose
Xs = zeros(nF, 3, 2);
for i=1:nF
    Xs(i,:,:) = project2Plane(V(F(i, :), :));
end

%% set up sparse complex matrix
A = (Xs(:, [3 1 2], 1) - Xs(:, [2 3 1], 1)) ./ AT_sq;   %% real part
B = (Xs(:, [3 1 2], 2) - Xs(:, [2 3 1], 2)) ./ AT_sq;   %% imag part

MA = sparse(repmat((1:nF)', 1, 3), F, A, nF, nV);
MB = sparse(repmat((1:nF)', 1, 3), F, B, nF, nV);

%% pin 2 points on the boundary
[~, ~, T] = pinBoundary(V, F);

%% swap columns, now the pinned points are the last 2 ones
MA = MA * T; MB = MB * T;

M = [MA -MB; MB MA];

Mf1 = M(:, 1:nV-2);  Mf2 = M(:, 1+nV:end-2);
Mp1 = M(:, nV-1:nV); Mp2 = M(:, end-1:end);

AM = [Mf1 -Mf2; Mf2 Mf1];
b  =-[Mp1 -Mp2; Mp2 Mp1] * [0; 1; 0; 0];

%% solve linear system
uv = AM \ b;
uv = reshape(uv, [nV-2 2]);

%% fix pinned points
uv = [uv; [0 0]; [1 0]];

%% transform back to original vertex index
uv = T * uv;

end
```

```matlab
function [b1, b2, T] = pinBoundary(V, F)
%% A helper function to pin 2 points on the boundary
%% Args:
%%      V[nV, 3]: vertices in 3D
%%      F[nF, 3]: face connectivity
%% Returns:
%%      b1: pinned boundary vertex
%%      b2: pinned boundary vertex
%%      T[nV, nV]: vertex index transform matrix

nV = size(V, 1);

[B, ~] = findBoundary(V, F);
nB = length(B);

%% select the first and middle boundary points
b1 = B(1); b2 = B(round(nB/2));

%% sparse index transform matrix
tripI = 1:nV; tripJ = 1:nV; tripV = ones(1, nV);
tripJ([b1 end-1]) = tripJ([end-1 b1]);
tripJ([b2 end])   = tripJ([end b2]);

T = sparse(tripI, tripJ, tripV, nV, nV);

end
```

## Mean Value Coordinates

```matlab
function uv = MVCTutte(V, F)
%% Tutte's embedding with mean value coordinates
%% Args:
%%      V[nV, 3]: vertices in 3D
%%      F[nF, 3]: face connectivity
%% Returns:
%%      uv[nV, 2]: uv coordinates

nV = size(V, 1);

[B, ~] = findBoundary(V, F);
nB = length(B);

%% LSCM to pin the boundary
uv = LSCM(V, F);

%% edges
E     = reshape(V(F(:, [2, 3, 1]), :) - V(F, :), [size(F), 3]);
Enorm = vecnorm(E, 2, 3);
Edir  = E ./ Enorm;

%% trigonometry
coss =-dot(Edir(:, :, :), Edir(:, [3, 1, 2], :), 3);
sins = vecnorm(cross(Edir(:, :, :), -Edir(:, [3, 1, 2], :), 3), 2, 3);

%% tan(theta/2) = sin(theta) / (1+cos(theta))
tanHalf = sins ./ (coss + 1);

%% set up linear system
tripI = [F F];
tripJ = [F(:, [2 3 1]) F(:, [3 1 2])];
tripV = [tanHalf ./ Enorm(:,:) tanHalf ./ Enorm(:, [3 1 2])];

A = sparse(tripI, tripJ, tripV, nV, nV);
A = A - diag(sum(A, 2));

%% pinned boundary points
A(B, :) = sparse(nB, nV);
A(B, B) = speye(nB);

b = zeros(nV, 2);
b(B,:) = uv(B, :);

%% solve linear system
uv = A \ b;

end
```

## Reference

- [Least Squares Conformal Maps for Automatic Texture Atlas Generation](https://members.loria.fr/Bruno.Levy/papers/LSCM_SIGGRAPH_2002.pdf)
- [Mean Value Coordinates](https://cgvr.informatik.uni-bremen.de/teaching/cg_literatur/barycentric_floater.pdf)
- [Discrete One-Forms on Meshes and Applications to 3D Mesh Parameterization](http://www.cs.harvard.edu/~sjg/papers/tutte.pdf)
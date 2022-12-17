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
---
layout: article
title: OMSCS-CV课程笔记09-Lightness and Brightness
tags: ["OMSCS", "CS6476-CV"]
key: OMSCS-CV-09
aside:
  toc: true
sidebar:
  nav: OMSCS-CV
---

> 这个系列是Gatech OMSCS 计算机视觉课程([CS 6476: Computer Vision](https://omscs.gatech.edu/cs-6476-computer-vision))的同步课程笔记。课程内容涉及图像处理以及传统计算机视觉的相关理论和方法，本节主要介绍光照和着色的相关内容。
<!--more-->

## Photometry

**光度学(photometry)**是研究光强弱的学科。对于三维空间中的物体，我们之所以能够看见它们是因为物体反射了光。反射光的强弱决定了我们看到的物体的颜色，而反射光则由物体法线、物体的材质、光照条件以及观察的角度所决定。

<div align=center>
<img src="https://i.imgur.com/ZOer74o.png" width="60%">
</div>

### Radiometry

如果想要更严格地描述反射的过程则需要借助**辐照度量学(radiometry)**的相关知识。我们定义**辐射率(radiance)**为单位立体角和**垂直**此方向的单位面积上的辐射通量，记为$L$(W⋅sr$^{−1}$⋅m$^{−2}$)；**辐照度(irradiance)**单位面积上接收到的辐射通量，记为$E$(W⋅m$^{−2}$)。radiance和irradiance可通过入射方向与法向的夹角$\theta$来进行转换：

$$
E(\theta, \varphi) = L(\theta, \varphi) \cos \theta \ d\omega
$$

<div align=center>
<img src="https://i.imgur.com/ZpYW7Oh.png" width="30%">
</div>

当光线照射到物体上时，物体反射出的radiance由**双向反射分布函数(bidirectional reflectance distribution function, BRDF)**控制，它定义为反射出的radiance与接收到的irradiance的比值：

$$
f(\theta_i, \varphi_i; \theta_r, \varphi_r) = \frac{L(\theta_r, \varphi_r)}{E(\theta_i, \varphi_i)}
$$

<div align=center>
<img src="https://i.imgur.com/az7L7iY.png" width="70%">
</div>

BRDF需要满足Helmholtz互异性(Helmholtz reciprocity)，即交换入射和出射方向函数值不变。同时BRDF还满足旋转对称性，即BRDF仅与入射和出射方向在平面上的相对夹角$\varphi_i - \varphi_r$有关，当入射方向和出射方向同时绕法向旋转时BRDF保持不变。

$$
f(\theta_i, \varphi_i; \theta_r, \varphi_r) = f(\theta_r, \varphi_r; \theta_i, \varphi_i)
$$

$$
f(\theta_i, \varphi_i; \theta_r, \varphi_r) = f(\theta_i, \theta_r; \varphi_i - \varphi_r)
$$

### Reflection Models

对于表面比较粗糙的物体，我们可以认为光线到达物体表面后会向各个方向发生反射，这种类型的反射称为**漫反射(diffuse reflection)**。

<div align=center>
<img src="https://i.imgur.com/nvhk9eG.png" width="50%">
</div>

另一种常见的反射类型是**镜面反射(surface reflection)**，此时反射会集中到某些指定的方向使得物体表面出现反光的效果。

<div align=center>
<img src="https://i.imgur.com/PNfmEhs.png" width="50%">
</div>

当然大多数情况下物体表面会同时发生漫反射和镜面反射。

<div align=center>
<img src="https://i.imgur.com/YvrBSi4.png" width="52%">
</div>

### Diffuse Reflection and Lambertian BRDF

漫反射的一个重要特征是无论观察的角度如何，漫反射的强度都是一样的。换句话说漫反射材质的BRDF是一个常数，我们称之为**反照率(albedo)：**

$$
f(\theta_i, \varphi_i; \theta_r, \varphi_r) = \rho_d
$$

我们将化简后的BRDF带入反射过程得到漫反射情况下反射的radiance：

$$
L = \rho_d I \cos \theta_i = \rho_d I (n \cdot s)
$$

<div align=center>
<img src="https://i.imgur.com/SFRrA3O.png" width="60%">
</div>

### Specular Reflection and Mirror BRDF

对于镜面反射的BRDF，我们可以利用$\delta$函数来描述只在给定方向上存在radiance的情况：

$$
f(\theta_i, \varphi_i; \theta_v, \varphi_v) = \rho_s \delta (\theta_i - \theta_v) \delta (\varphi_i + \pi - \varphi_v)
$$

类似地，镜面反射出的radiance为：

$$
L = \rho_s I \delta(m - v)
$$

<div align=center>
<img src="https://i.imgur.com/9G7olsF.png" width="67%">
</div>

### Phong Reflection Model

我们把漫反射和镜面反射结合到一起就得到了图形渲染中非常常用的Phong反射模型，它将漫反射和镜面反射相加来模拟真实材质的BRDF。

<div align=center>
<img src="https://i.imgur.com/qqB029q.png" width="50%">
</div>

## Lightness

## Shape from Shading
---
layout: article
title: OMSCS-GA课程笔记01-Dynamic Programming
tags: ["OMSCS", "CS6515-GA"]
key: OMSCS-GA-01
aside:
  toc: true
sidebar:
  nav: OMSCS-GA
---

> 这个系列是Gatech OMSCS 高级算法课程([CS 6515: Intro to Grad Algorithms](https://omscs.gatech.edu/cs-6515-intro-graduate-algorithms))的同步课程笔记。课程内容涉及强化学习算法的理论和相关应用，本节主要介绍动态规划。
<!--more-->

**动态规划(dynamic programming, DP)**是算法设计中非常重要的一种思想，很多复杂的问题都可以基于动态规划来进行求解。

## Fibonacci Numbers

计算Fibonacci数列是一个经典的算法问题。Fibonacci数列的递推式为：

$$
F_0 = 0, \ F_1 = 1 \\
F_n = F_{n-2} + F_{n-1}, \ \text{for} \ n \geq 2
$$

我们的目标是对于任意的整数$n \geq 0$，输出第$n$项数值$F_n$。

### Recursive Algorithm

显然我们可以使用递归的方式来求解这个问题：

```
Fib1(n):
    if n == 0
        return 0
    if n == 1
        return Fib1(n-1) + Fib1(n-2)
```

根据主定理我们可以计算这个算法的复杂度：

$$
T(n) \leq O(1) + T(n-1) + T(n-2)
$$

$$
T(n) \geq F_n \approx \frac{\phi^n}{\sqrt{5}}
$$

其中$\phi=\frac{1+\sqrt{5}}{2} \approx 1.618$，即该算法有指数级的复杂度。

显然`Fib1(n)`不是一个好的算法，其问题在于它会反复计算数列前面的项。

<div align=center>
<img src="https://i.imgur.com/QBssznj.png" width="80%">
</div>

### DP Algorithm

接下来我们使用动态规划来改进之前的算法。具体地，我们使用一个数组来存储中间的计算结果然后从前向后进行计算：

```
Fib2(n):
    F[0] = 0
    F[1] = 1

    for i=2:n
        F[i] = F[i-1] + F[i-2]
    
    return F[n]
```

显然此时算法的复杂度为$O(n)$，远小于之前的复杂度。

从这个例子可以看出动态规划的特点：

<div align=center>
<img src="https://i.imgur.com/MmQlu6J.png" width="80%">
</div>

## Longest Increasing Subsequence

LIS问题的目标是在给定序列中寻找递增子列的长度，注意这里我们允许对原始序列进行删减来获得子列。

<div align=center>
<img src="https://i.imgur.com/InNHqpl.png" width="80%">
</div>

### Subproblem Attempt

使用DP的步骤是首先定义一个subproblem，然后依次求解subproblem。

<div align=center>
<img src="https://i.imgur.com/OrvDRcO.png" width="80%">
</div>

对于LIS问题可以进行形式化如下：

<div align=center>
<img src="https://i.imgur.com/nH3zrPE.png" width="80%">
</div>

### Recurrence Attempt

求解LIS问题的核心在于记录下序列中每个元素结尾时递增子列的长度。

<div align=center>
<img src="https://i.imgur.com/UpO1clv.png" width="80%">
</div>

<div align=center>
<img src="https://i.imgur.com/wecKkrK.png" width="80%">
<img src="https://i.imgur.com/mSrPH3M.png" width="80%">
</div>

### DP Algorithm

因此我们可以基于DP来设计算法：

```
LIS(a[]):
    for i=1:n
        L[i] = 1

        for j=1:i-1
            if a[j] < a[i] & L[i] < 1+L[j]
                L[i] = 1 + L[j]

    max = 1
    for i=2:n
        if L[i] > L[max]
            max = i

    return max
```

此时算法的复杂度为$O(n^2)$。

## Longest Common Subsequence

LCS问题的目标是计算两个序列中最长的公共子列：

<div align=center>
<img src="https://i.imgur.com/bA8GydQ.png" width="80%">
</div>

### Subproblem Attempt1

<div align=center>
<img src="https://i.imgur.com/7kqzCSh.png" width="80%">
</div>

### Recurrence Attempt1

<div align=center>
<img src="https://i.imgur.com/2q0zgaA.png" width="80%">
<img src="https://i.imgur.com/JTJvkbb.png" width="80%">
</div>

### Subproblem Attempt2

<div align=center>
<img src="https://i.imgur.com/7ts0xtJ.png" width="80%">
</div>

### Recurrence Attempt2

<div align=center>
<img src="https://i.imgur.com/hW9KwqY.png" width="80%">
<img src="https://i.imgur.com/YJjLKVP.png" width="80%">
<img src="https://i.imgur.com/YueOEWA.png" width="80%">
<img src="https://i.imgur.com/dLDg8o9.png" width="80%">
</div>

### DP Algorithm

因此求解LCS的算法为：

```
LCS(X[], Y[]):
    for i=0:n
        L[i, 0] = 0
    for j=0:n
        L[0, j] = 0
    
    for i=1:n
        for j=1:n
            if X[i] == Y[j]
                L[i, j] = 1 + L[i-1, j-1]
            else
                L[i, j] = max(L[i, j-1], L[i-1, j])
    
    return L[n, n]
```

此时算法的复杂度为$O(n^2)$。

如果想要获得最长公共子列，还可以从L的右下角开始向上进行追溯：

<div align=center>
<img src="https://i.imgur.com/6KeLTki.png" width="80%">
</div>

## Knapsack

## Chain Matrix Multiply

## Shortest Path Algorithms
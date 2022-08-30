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

knapsack是经典的优化问题，我们希望在一定的约束下最大化最大价值：

<div align=center>
<img src="https://i.imgur.com/AqMxn1p.png" width="80%">
</div>

### Greedy Algorithm

贪心算法是求解knapsack问题的一种经典解法，不过需要注意的是贪心算法往往不能得到问题的最优解。

<div align=center>
<img src="https://i.imgur.com/4RaHtnI.png" width="80%">
</div>

### Attempt1

<div align=center>
<img src="https://i.imgur.com/rGEnwFr.png" width="80%">
<img src="https://i.imgur.com/l53NiJl.png" width="80%">
</div>

### Attempt2

<div align=center>
<img src="https://i.imgur.com/hvBRfA4.png" width="80%">
<img src="https://i.imgur.com/zllCzsN.png" width="80%">
</div>

### DP Algorithm

因此，使用DP来求解knapsack问题的伪代码如下：

```
KnapsackNoRepeat(w[], v[], B):
    for b=0:B
        K[0, b] = 0
    for i=1:n
        K[i, 0] = 0
    
    for i=1:n
        for b=1:B
            if w[i] <= b
                K[i, b] = max(v[i]+K[i-1, b-w[i]], K[i-1, b])
            else
                K[i, b] = K[i-1, b]
    
    return K[i, b]
```

此时算法的复杂度为$O(nB)$。这里需要说明的是$O(nB)$依赖于限制$B$的值，而要表示$B$则需要$O(\log B)$的空间。因此这个算法并不是一个非常高效的算法。实际上人们已经证明knapsack问题是NP-complete，我们目前无法找到一个高效的解法。

<div align=center>
<img src="https://i.imgur.com/CHzHAfM.png" width="80%">
</div>

### Knapsack Repetition

<div align=center>
<img src="https://i.imgur.com/TWsPpKo.png" width="80%">
<img src="https://i.imgur.com/edTQSrR.png" width="80%">
</div>

#### Simpler Subproblem

<div align=center>
<img src="https://i.imgur.com/zxxW6cI.png" width="80%">
</div>

因此对于允许重复的knapsack问题可以按照如下过程进行求解：

```
KnapsackRepeat(w[], v[], B):
    for b=0:B
        K[b] = 0

        for i=1:n
            if w[i] <= b & K[b] < v[i]+K[b-w[i]]
                K[b] = v[i] + K[b-w[i]]
    
    return K[B]
```

此时算法的复杂度为$O(nB)$，仍然不是一个高效的解法。

## Chain Matrix Multiply

### Motivation

动态规划还可以用来处理矩阵乘法。回忆矩阵乘法的运算规则，新矩阵的每个元素都是$A$和$B$矩阵对应行列的内积。

<div align=center>
<img src="https://i.imgur.com/6uXt8oz.png" width="80%">
</div>

由于矩阵乘法的结合性，对于链式相乘的矩阵我们可以调整矩阵乘法的计算顺序从而改变整个乘法的计算复杂度。

<div align=center>
<img src="https://i.imgur.com/w1C3UOG.png" width="80%">
</div>

具体地，对于矩阵乘法$Z_{a \times c} = W_{a \times b} \cdot Y_{b \times c}$的计算复杂度为$O(abc)$。

<div align=center>
<img src="https://i.imgur.com/ujk2c9q.png" width="80%">
</div>

### General Problem

因此，连续矩阵相乘的问题就可以使用动态规划的思路进行建模。

<div align=center>
<img src="https://i.imgur.com/vXBBgca.png" width="80%">
</div>

### Graphical View

同时我们也可以使用二叉树来理解计算的过程，而我们的目标则是找到总体代价最小的树。

<div align=center>
<img src="https://i.imgur.com/s2l9PYS.png" width="80%">
</div>

### Substring

<div align=center>
<img src="https://i.imgur.com/w40ZPsG.png" width="80%">
<img src="https://i.imgur.com/k6jcry4.png" width="80%">
<img src="https://i.imgur.com/gMQp4mA.png" width="80%">
<img src="https://i.imgur.com/5PLssSE.png" width="80%">
<img src="https://i.imgur.com/2IiCARh.png" width="80%">
</div>

### DP Algorithm

因此使用动态规划矩阵相乘计算最小复杂度的核心是从对角线开始逐步向上进行递推，它和上面介绍过的其它动态规划递推方法有显著区别。

```
ChainMultiply(m0, m1, ..., mn):
    for i=1:n
        C[i, i] = 0
    
    for s=1:n-1
        for i=1:n-s
            j=i+s
            C[i, j] = inf

            for l=1:j-1
                cur = m[i-1]*m[l]*m[j] + C[i, l] + C[l+1, j]
                if cur < C[i, j]
                    C[i, j] = cur
    
    return C[1, n]
```

整个算法的复杂度为$O(n^3)$。

<div align=center>
<img src="https://i.imgur.com/m7cWQsf.png" width="80%">
</div>

## Shortest Path Algorithms
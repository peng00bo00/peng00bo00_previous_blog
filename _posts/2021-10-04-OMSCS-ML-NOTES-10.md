---
layout: article
title: OMSCS-ML课程笔记10-Randomized Optimization
tags: ["OMSCS", "CS7641-ML"]
key: OMSCS-ML-10
aside:
  toc: true
sidebar:
  nav: OMSCS-ML
---

> 这个系列是Gatech OMSCS 机器学习课程([CS 7641: Machine Learning](https://omscs.gatech.edu/cs-7641-machine-learning))的同步课程笔记。课程内容涉及监督学习、无监督学习和强化学习三个部分，本节主要介绍随机优化的相关内容。
<!--more-->

机器学习中的很多算法都可以抽象成一个优化问题。对于连续型变量的优化问题，我们可以通过梯度下降、牛顿法等算法来高效的求解。但对于离散变量的优化问题我们无法计算导数，因此不能使用这些算法。本节将介绍一些常用的随机优化算法来求解这样的离散优化问题，为便于讨论这里均假定带求解的问题是一个最大化问题。

## Hill Climbing

Hill Climbing是最简单的优化算法。假设我们当前位于$x$处，hill climbing算法会搜索$x$附件的所有点并移动到函数$f$取最大值的位置，如果$x$周围的其它点函数值都小于当前点则认为已经找到了最大值。

显然hill climbing算法不能处理局部极值的情况，因此在实际应用中往往会结合随机重启来避免局部极值点。此时算法会执行若干次标准hill climbing，每次找到极值点就会记录当前位置并重置初始位置。算法最终返回的结果为这些记录中的最大值。这样的算法也称为random hill climbing算法。

## Simulated Annealing

**模拟退火(simulated annealing)**是另一种常用的优化算法。与hill climbing算法相比，模拟退火会尝试跳出当前点的邻域从而避免陷入局部极值的问题。模拟退火的算法框架如下：

1. 初始化当前位置$x = x_0$；
2. 更新当前温度$T = \alpha T$；
3. 选择一个随机邻居$x'$并计算$f(x')$：；
   1. 如果$f(x') \gt f(x)$则更新当前位置$x = x'$；
   2. 否则按概率$$p = \exp \{ \frac{f(x') - f(x)}{T} \}$$更新当前位置$x = x'$；
4. 返回第2步直至达到指定的循环次数。

在开始的循环中温度$T$比较大，此时转移概率$p$接近于1使得算法倾向于在状态空间中进行随机跳跃来寻找最优点。而随着循环次数的增加，转移概率$p$由函数差值$f(x') - f(x)$控制，仅在函数值有较大变化时才会进行跳转，此时算法会更接近于在当前点附近进行搜索。

模拟退火算法的结果与初始值$x_0$无关，而且当退火时间足够长的情况下会以概率1收敛到全局最大值。

## Genetic Algorithms

**遗传算法(genetic algorithms)**是一种经典的优化算法，它的思想来源于生物种群的演化过程。遗传算法的基本框架如下：

1. 初始化种群中的个体数量；
2. 计算每个个体的适应性；
3. 选择适应性较高的一部分个体进行交配(crossover)，得到子代个体；
4. 返回第2步直至达到指定的循环次数。

从算法框架中不难发现遗传算法的核心在于选择适应性较高的个体并进行交配这一步。在实践中的常用做法是将种群中每个个体的适应性转换为概率并进行抽样作为亲代，同时对亲代的状态向量$x$进行随机组合来获得子代。此外对于子代的状态向量往往还会进行随机突变来提高种群中个体的多样性。

遗传算法在大多数情况下都能获得比较合理的解，但它的难点一般在于如何将问题建模成遗传算法可以求解的形式。

## MIMIC

## Reference

- [Wikipedia: Hill climbing](https://en.wikipedia.org/wiki/Hill_climbing)
- [Wikipedia: Simulated annealing](https://en.wikipedia.org/wiki/Simulated_annealing)
- [Wikipedia: Genetic algorithm](https://en.wikipedia.org/wiki/Genetic_algorithm)
- [MLROSE.Algorithms](https://mlrose.readthedocs.io/en/stable/_modules/mlrose/algorithms.html)
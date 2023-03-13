---
layout: article
title: 动态规划
key: leetcode-10
clipboard: true
aside:
  toc: true
sidebar:
  nav: LeetCode
---

**动态规划(dynamic programming, DP)**是利用子问题之间的关系来递推出整个问题的解。一般来说DP问题可以分解为一下五步来求解：

1. 确定`dp`数组(dp table)以及下标的含义
2. 确定递推公式
3. `dp`数组如何初始化
4. 确定遍历顺序
5. 举例推导dp数组

## 基础题目

### 509. 斐波那契数

**斐波那契数**(通常用`F(n)`表示)形成的序列称为**斐波那契数列**。该数列由`0`和`1`开始，后面的每一项数字都是前面两项数字的和。也就是：

```
F(0) = 0，F(1) = 1
F(n) = F(n - 1) + F(n - 2)，其中 n > 1
```

给定`n`，请计算`F(n)`。

**示例1：**

```
输入：n = 2
输出：1
解释：F(2) = F(1) + F(0) = 1 + 0 = 1
```

**示例2：**

```
输入：n = 3
输出：2
解释：F(3) = F(2) + F(1) = 1 + 1 = 2
```

**示例3：**

```
输入：n = 4
输出：3
解释：F(4) = F(3) + F(2) = 2 + 1 = 3
```

**提示：**

- 0 <= `n` <= 30

#### Solution

求斐波那契数是DP的经典问题。我们建立一个数组`dp[]`用来表示数列，其中`dp[i]`即为`F(i)`。此外，题目中已经给出了初始化条件和递推关系：

- `dp[0] = 0`，`dp[1] = 1`
- `dp[i] = dp[i-2] + dp[i-1]`

这样我们就只需要直接递推即可。

[题目链接](https://leetcode.cn/problems/fibonacci-number/)：

```python
class Solution:
    def fib(self, n: int) -> int:
        if n == 0:
            return 0
        elif n == 1:
            return 1

        dp = [0 for _ in range(n+1)]
        dp[1] = 1

        for i in range(2, n+1):
            dp[i] = dp[i-2] + dp[i-1]
        
        return dp[-1]
```
{: .snippet}

除了上述标准解法外，我们还可以只需要使用两个变量来进行递推而无需记录整个数组。这种解法的空间复杂度为`O(1)`。

[题目链接](https://leetcode.cn/problems/fibonacci-number/)：

```python
class Solution:
    def fib(self, n: int) -> int:
        if n == 0:
            return 0
        elif n == 1:
            return 1

        pre, cur = 0, 1
        for i in range(n-1):
            pre, cur = cur, pre+cur
        
        return cur
```
{: .snippet}

### 70. 爬楼梯

假设你正在爬楼梯。需要`n`阶你才能到达楼顶。

每次你可以爬`1`或`2`个台阶。你有多少种不同的方法可以爬到楼顶呢？

**示例1：**

```
输入：n = 2
输出：2
解释：有两种方法可以爬到楼顶。
1. 1 阶 + 1 阶
2. 2 阶
```

**示例2：**

```
输入：n = 3
输出：3
解释：有三种方法可以爬到楼顶。
1. 1 阶 + 1 阶 + 1 阶
2. 1 阶 + 2 阶
3. 2 阶 + 1 阶
```

**提示：**

- 1 <= `n` <= 45

#### Solution

爬楼梯同样是DP的经典问题。我们建立一个数组`dp[]`，其中`dp[i]`为爬到第`i-1`阶楼梯的最短方式。本题的初始化条件和递推关系为：

- `dp[0] = 1`，`dp[1] = 2`
- `dp[i] = dp[i-2] + dp[i-1]`

这样我们就只需要直接递推即可。

[题目链接](https://leetcode.cn/problems/climbing-stairs/)：

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 1:
            return 1
        elif n == 2:
            return 2
        
        dp = [0 for i in range(n)]
        dp[0] = 1
        dp[1] = 2

        for i in range(2, n):
            dp[i] = dp[i-2] + dp[i-1]
        
        return dp[-1]
```
{: .snippet}

类似于[斐波那契数](/leetcode/2023-03-13-DynamicProgramming.html#509-斐波那契数)，我们同样可以使用`O(1)`的空间复杂度来进行递推。

[题目链接](https://leetcode.cn/problems/climbing-stairs/)：

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 1:
            return 1
        elif n == 2:
            return 2
        
        pre, cur = 1, 2

        for i in range(n-2):
            pre, cur = cur, pre+cur
        
        return cur
```
{: .snippet}

### 746. 使用最小花费爬楼梯

给你一个整数数组`cost`，其中`cost[i]`是从楼梯第`i`个台阶向上爬需要支付的费用。一旦你支付此费用，即可选择向上爬一个或者两个台阶。

你可以选择从下标为`0`或下标为`1`的台阶开始爬楼梯。

请你计算并返回达到楼梯顶部的最低花费。

**示例1：**

```
输入：cost = [10,15,20]
输出：15
解释：你将从下标为 1 的台阶开始。
- 支付 15 ，向上爬两个台阶，到达楼梯顶部。
总花费为 15 。
```

**示例2：**

```
输入：cost = [1,100,1,1,1,100,1,1,100,1]
输出：6
解释：你将从下标为 0 的台阶开始。
- 支付 1 ，向上爬两个台阶，到达下标为 2 的台阶。
- 支付 1 ，向上爬两个台阶，到达下标为 4 的台阶。
- 支付 1 ，向上爬两个台阶，到达下标为 6 的台阶。
- 支付 1 ，向上爬一个台阶，到达下标为 7 的台阶。
- 支付 1 ，向上爬两个台阶，到达下标为 9 的台阶。
- 支付 1 ，向上爬一个台阶，到达楼梯顶部。
总花费为 6 。
```

**提示：**

- 2 <= `cost.length` <= 1000
- 0 <= `cost[i]` <= 999

#### Solution

本题类似于[爬楼梯](/leetcode/2023-03-13-DynamicProgramming.html#70-爬楼梯)，但要稍微复杂一些。我们建立一个数组`dp[]`，其中`dp[i]`为爬到第`i`阶楼梯的最小代价。由于我们可以选择下标为`0`或下标为`1`的台阶开始爬楼梯，因此数组`dp[]`需要初始化如下：

- `dp[0] = 0`，`dp[1] = 0`

接下来考虑递推关系，我们可以从第`i-2`阶或是第`i-1`阶向上爬。根据题意，最小代价而二者中较小的那个：

- `dp[i] = min(dp[i-2] + cost[i-2], dp[i-1] + cost[i-1])`

得到递推关系后直接进行递推即可。

[题目链接](https://leetcode.cn/problems/min-cost-climbing-stairs/)：

```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        N = len(cost)

        dp = [0 for i in range(N+1)]

        for i in range(2, N+1):
            dp[i] = min(dp[i-2] + cost[i-2], dp[i-1] + cost[i-1])
        
        return dp[-1]
```
{: .snippet}

本题同样可以使用`O(1)`的空间复杂度来进行求解。

[题目链接](https://leetcode.cn/problems/min-cost-climbing-stairs/)：

```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        N = len(cost)
        pre = cur = 0

        for i in range(2, N+1):
            pre, cur = cur, min(pre+cost[i-2], cur+cost[i-1])
        
        return cur
```
{: .snippet}

## 背包问题

## 打家劫舍

## 股票问题

## 子序列问题

## Reference

- [动态规划理论基础](https://www.bilibili.com/video/BV13Q4y197Wg/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：509.斐波那契数](https://www.bilibili.com/video/BV1f5411K7mo/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：70.爬楼梯](https://www.bilibili.com/video/BV17h411h7UH/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：746.使用最小花费爬楼梯](https://www.bilibili.com/video/BV16G411c7yZ/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
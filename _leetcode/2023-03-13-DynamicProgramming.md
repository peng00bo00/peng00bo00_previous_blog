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

**动态规划(dynamic programming, DP)**是利用子问题之间的关系来递推出整个问题的解。一般来说DP问题可以分解为以下五步来求解：

1. 确定`dp`数组(dp table)以及下标的含义
2. 确定递推公式
3. `dp`数组如何初始化
4. 确定遍历顺序
5. 举例推导`dp`数组

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

### 62. 不同路径

一个机器人位于一个`m x n`网格的左上角(起始点在下图中标记为“Start”)。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角(在下图中标记为“Finish”)。

问总共有多少条不同的路径？

<div align=center>
<img src="https://images.weserv.nl/?url=assets.leetcode.com/uploads/2018/10/22/robot_maze.png">
</div>

**示例1：**

```
输入：m = 3, n = 7
输出：28
```

**示例2：**

```
输入：m = 3, n = 2
输出：3
解释：
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右
3. 向下 -> 向右 -> 向下
```

**示例3：**

```
输入：m = 7, n = 3
输出：28
```

**示例4：**

```
输入：m = 3, n = 3
输出：6
```

**提示：**

- 1 <= `m`, `n` <= 100
- 题目数据保证答案小于等于`2 * 10⁹`

#### Solution

本题中我们需要使用一个二维数组`dp[][]`，其中每一个元素`dp[i][j]`表示从`[0][0]`到`[i][j]`位置有多少种路径。根据题意我们只能从左边`[i-1][j]`或者上边`[i][j-1]`前往`[i][j]`，因此动态规划的递推关系为：

- `dp[i][j] = dp[i-1][j] + dp[i][j-1]`

接下来考虑初始条件。对于数组`dp[][]`的第一行和第一列，我们只能一直向右或是一直向下前进，即只有一条路径。因此我们可以把数组`dp[][]`的所有元素都初始化为`1`，然后从`dp[1][1]`开始向右和向下进行递推。

[题目链接](https://leetcode.cn/problems/unique-paths/)：

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[1 for _ in range(n)] for _ in range(m)]

        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i-1][j] + dp[i][j-1]

        return dp[-1][-1]
```
{: .snippet}

当然本题的空间复杂度也可以进行优化，实际上我们只需要维护`dp[][]`的一行或者一列即可。

[题目链接](https://leetcode.cn/problems/unique-paths/)：

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [1 for i in range(n)]

        for i in range(1, m):
            for j in range(1, n):
                dp[j] += dp[j-1]

        return dp[-1]
```
{: .snippet}

### 63. 不同路径 II

一个机器人位于一个`m x n`网格的左上角(起始点在下图中标记为“Start”)。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角(在下图中标记为“Finish”)。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

网格中的障碍物和空位置分别用`1`和`0`来表示。

**示例1：**

<div align=center>
<img src="https://images.weserv.nl/?url=assets.leetcode.com/uploads/2020/11/04/robot1.jpg">
</div>

```
输入：obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
输出：2
解释：3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右
```

**示例2：**

<div align=center>
<img src="https://images.weserv.nl/?url=assets.leetcode.com/uploads/2020/11/04/robot2.jpg">
</div>

```
输入：obstacleGrid = [[0,1],[0,0]]
输出：1
```

**提示：**

- `m` == `obstacleGrid.length`
- `n` == `obstacleGrid[i].length`
- 1 <= `m, n` <= 100
- `obstacleGrid[i][j]`为`0`或`1`

#### Solution

本题类似于[不同路径](/leetcode/2023-03-13-DynamicProgramming.html#62-不同路径)，不过由于障碍的存在我们在初始化和递推时需要一些额外的注意。在初始化时我们不能直接将`dp[][]`的第一行和第一列初始化为`1`，而是要通过从左到右从上到下的顺序进行初始化。如果在某个位置遇到了障碍后面的位置会被挡住，因此我们需要结束初始化。完成初始化后需要按照递推公式进行递推：

- `dp[i][j] = dp[i-1][j] + dp[i][j-1]`

需要注意的是我们同样需要越过有障碍的位置，让有障碍的位置满足`dp[i][j] == 0`。

[题目链接](https://leetcode.cn/problems/unique-paths-ii/)：

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        if obstacleGrid[0][0]:
            return 0
        
        m = len(obstacleGrid)
        n = len(obstacleGrid[0])

        dp = [[0 for _ in range(n)] for _ in range(m)]
        dp[0][0] = 1

        for i in range(m):
            if obstacleGrid[i][0]:
                break
            dp[i][0] = 1
        
        for j in range(n):
            if obstacleGrid[0][j]:
                break
            dp[0][j] = 1

        for i in range(1, m):
            for j in range(1, n):
                if obstacleGrid[i][j] == 0:
                    dp[i][j] = dp[i-1][j] + dp[i][j-1]
        
        return dp[-1][-1]
```
{: .snippet}

使用一维数组来进行递推的解法可参考如下。

[题目链接](https://leetcode.cn/problems/unique-paths-ii/)：

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        if obstacleGrid[0][0]:
            return 0
        
        m = len(obstacleGrid)
        n = len(obstacleGrid[0])

        dp = [0 for _ in range(n)]
        dp[0] = 1

        ## initialize first row
        for j in range(n):
            if obstacleGrid[0][j]:
                break
            dp[j] = 1

        for i in range(1, m):
            for j in range(n):
                if obstacleGrid[i][j]:
                    dp[j] = 0
                elif j > 0:
                    dp[j] += dp[j-1]
        
        return dp[-1]
```
{: .snippet}

### 343. 整数拆分

给定一个正整数`n`，将其拆分为`k`个**正整数**的和(`k` >= 2)，并使这些整数的乘积最大化。

返回你可以获得的**最大乘积**。

**示例1：**

```
输入: n = 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1。
```

**示例2：**

```
输入: n = 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36。
```

**提示：**

- 2 <= `n` <= 58

#### Solution

本题的难点在于动态规划的递推关系。我们建立一个数组`dp[]`，其中`dp[i]`表示整数`i`可以拆分成的最大乘积。显然有初始条件：

- `dp[2]` = 1

接下来考虑递推关系。假设正整数`i`拆分出的第一个数为`j`，则`dp[i]`有以下两种可能：

1. 将`i`拆分为`j`和`i-j`，此时乘积为`j*(i-j)`
2. 继续对`i-j`进行拆分，这部分乘积的最大值为`dp[i-j]`，因此拆分后所有部分的乘积为`j*dp[i-j]`

因此我们需要对这两种情况的乘积取最大值，得到递推关系：

- `dp[i] = max([dp[i], j*(i-j), j*dp[i-j]])`

这样只需要在递推时对`j`进行遍历然后一直取`dp[i]`的最大值即可。

[题目链接](https://leetcode.cn/problems/integer-break/)：

```python
class Solution:
    def integerBreak(self, n: int) -> int:
        dp = [0 for _ in range(n+1)]
        dp[2] = 1

        for i in range(2, n+1):
            for j in range(1, i):
                dp[i] = max(dp[i], j*(i-j), j*dp[i-j])

        return dp[-1]
```
{: .snippet}

### 96. 不同的二叉搜索树

给你一个整数`n`，求恰由`n`个节点组成且节点值从`1`到`n`互不相同的**二叉搜索树**有多少种？返回满足题意的二叉搜索树的种数。

**示例1：**

<div align=center>
<img src="https://images.weserv.nl/?url=assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg">
</div>

```
输入：n = 3
输出：5
```

**示例2：**

```
输入：n = 1
输出：1
```

**提示：**

- 1 <= `n` <= 19

#### Solution

本题的难点在于动态规划的递推关系。我们建立一个数组`dp[]`，其中`dp[i]`表示`[1, i]`所能构成的最多二叉搜索树的数目。假设某一个二叉搜索树的根节点为`1 <= j <= i`，则其左子树的可能数量为`dp[j-1]`，而右子树的数量则为`dp[i-j]`。这样以`j`为根节点的二叉搜索树的数目为`dp[j-1] * dp[i-j]`，我们对`j`进行遍历可以得到递推关系：

- `dp[i] += dp[j-1] * dp[i-j]`

接下来考虑初始条件。显然由`1`只能构成一棵二叉搜索树，而空节点也只能对应一棵二叉搜索树，即：

- `dp[0] = 1`，`dp[1] = 1`

这样只需要对`i`进行递推，同时对`j`进行遍历即可。

[题目链接](https://leetcode.cn/problems/unique-binary-search-trees/)：

```python
class Solution:
    def numTrees(self, n: int) -> int:
        dp = [0 for _ in range(n+1)]
        dp[0] = 1
        dp[1] = 1

        for i in range(2, n+1):
            for j in range(1, i+1):
                dp[i] += dp[j-1] * dp[i-j]
        
        return dp[-1]
```
{: .snippet}

## 背包问题

### 01背包

**01背包问题(01 knapsack problem)**是背包问题中最基础的问题，它可以表述为一共有`N`件物品其中每个物品的重量和价值分别为`w[i]`和`v[i]`。每件物品**只能用一次**，我们的目标是在保证物品的总重量不超过背包上限`W`的情况下计算包内物品的最大价值。

<div align=center>
<img src="https://images.weserv.nl/?url=i.imgur.com/Lr5L3HI.png" width="50%">
</div>

使用动态规划求解01背包问题时我们需要建立一个二维数组`dp[][]`，它的行数等于物品数、列数等于背包的容量、每个元素`dp[i][j]`表示背包容量为`j`且选择了`[0:i]`号物品情况下背包中物品的最大价值。

<div align=center>
<img src="https://images.weserv.nl/?url=i.imgur.com/zeQnAmr.png" width="70%">
</div>

接下来考虑递推关系。`dp[i][j]`对于物品`i`存在两种情况：

1. 物品`i`不在背包中，此时放不放物品`i`都不会影响包内的最大价值，即`dp[i][j] = dp[i-1][j]`
2. 物品`i`在背包中，此时包内的价值等于选择了`[0:i-1]`号物品且包内容量为`j-w[i]`情况下的最大价值加上物品`i`的价值，即`dp[i][j] = dp[i-1][j-w[i]] + v[i]`

以上两种情况取最大值，进而得到递推公式：

- `dp[i][j] = max(dp[i-1][j], dp[i-1][j-w[i]] + v[i])`

然后考虑`dp[][]`数组的初始化。显然当背包容量为`0`时无法放入任何物品，即最大价值为`0`。因此我们需要将`dp[][]`数组的第一列初始化为`0`，当然也可以直接把所有元素都初始化为`0`。

<div align=center>
<img src="https://images.weserv.nl/?url=i.imgur.com/1ONEPyC.png" width="70%">
</div>

而第一行要根据`0`号物品的重量来考虑，当`j >= w[0]`时令`dp[0][j] = v[0]`。

```python
for j in range(W):
    if j >= w[0]:
        dp[0][j] = v[0]
```

<div align=center>
<img src="https://images.weserv.nl/?url=i.imgur.com/HcT1DTY.png" width="70%">
</div>

最后从左上角向右向下进行递推即可，`dp[][]`数组的最后一个元素即为所求。

```python
for i in range(1, N):
    for j in range(1, W+1):
        if j >= w[i]:
            dp[i][j] = max(dp[i-1][j], dp[i-1][j-w[i]] + v[i])
        else:
            dp[i][j] = dp[i-1][j]
```

当然上述递推过程可以优化为只使用一维`dp[]`数组，实际上我们只需要维护原来二维数组的一行即可。此时的递推公式为：

- `dp[j] = max(dp[j], dp[j - w[i]]+v[i])`

不过需要注意的是一维的情况必须要**倒序遍历容量`j`**，这样才能保证物品只会被添加一次。

```python
for i in range(N):
    for j in range(W, w[i] - 1, -1):
        dp[j] = max(dp[j], dp[j - w[i]] + v[i])
```

### 416. 分割等和子集

给你一个**只包含正整数**的**非空**数组`nums`。请你判断是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

**示例1：**

```
输入：nums = [1,5,11,5]
输出：true
解释：数组可以分割成 [1, 5, 5] 和 [11] 。
```

**示例2：**

```
输入：nums = [1,2,3,5]
输出：false
解释：数组不能分割成两个元素和相等的子集。
```

**提示：**

- 1 <= `nums.length` <= 200
- 1 <= `nums[i]` <= 100

#### Solution

本题可以转换为在`nums`中寻找一个子集，使其和为`nums`总和的一半`target = sum(nums) // 2`。我们可以把这样的问题抽象为一个01背包问题，它的背包容量为`target`且每个物品的价值和重量都是`nums[i]`。如果背包恰好装满、最大价值恰好为`target`则说明可以把`nums`分割为等和的子集。

[题目链接](https://leetcode.cn/problems/partition-equal-subset-sum/)：

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        N = len(nums)
        if N < 2:
            return False

        if sum(nums) % 2 :
            return False
        
        target = sum(nums) // 2

        dp = [[0 for j in range(target+1)] for i in range(N)]

        for j in range(target+1):
            if j >= nums[0]:
                dp[0][j] = nums[0]

        for i in range(1, N):
            for j in range(1, target+1):
                if j >= nums[i]:
                    dp[i][j] = max(dp[i-1][j], dp[i-1][j - nums[i]]+nums[i])
                else:
                    dp[i][j] = dp[i-1][j]
        
        return dp[-1][-1] == target
```
{: .snippet}

本题的一维数组递推代码可参考如下。

[题目链接](https://leetcode.cn/problems/partition-equal-subset-sum/)：

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        N = len(nums)
        if N < 2:
            return False

        if sum(nums) % 2 :
            return False
        
        target = sum(nums) // 2

        dp = [0 for j in range(target+1)]

        for i in range(N):
            for j in range(target, nums[i]-1, -1):
                dp[j] = max(dp[j], dp[j - nums[i]] + nums[i])
        
        return dp[-1] == target
```
{: .snippet}

### 1049. 最后一块石头的重量 II

有一堆石头，用整数数组`stones`表示。其中`stones[i]`表示第`i`块石头的重量。

每一回合，从中选出任意两块石头，然后将它们一起粉碎。假设石头的重量分别为`x`和`y`，且`x <= y`。那么粉碎的可能结果如下：

- 如果`x == y`，那么两块石头都会被完全粉碎；
- 如果`x != y`，那么重量为`x`的石头将会完全粉碎，而重量为`y`的石头新重量为`y-x`。

最后，**最多只会剩下一块**石头。返回此石头**最小的可能重量**。如果没有石头剩下，就返回`0`。

**示例1：**

```
输入：stones = [2,7,4,1,8,1]
输出：1
解释：
组合 2 和 4，得到 2，所以数组转化为 [2,7,1,8,1]，
组合 7 和 8，得到 1，所以数组转化为 [2,1,1,1]，
组合 2 和 1，得到 1，所以数组转化为 [1,1,1]，
组合 1 和 1，得到 0，所以数组转化为 [1]，这就是最优值。
```

**示例2：**

```
输入：stones = [31,26,33,21,40]
输出：5
```

**提示：**

- 1 <= `stones.length` <= 30
- 1 <= `stones[i]` <= 100

#### Solution

本题可以理解为将`stones`分成两个和尽可能相等的子集，这样就可以使用的[分割等和子集](/leetcode/2023-03-13-DynamicProgramming.html#416-分割等和子集)思路来进行求解。此时背包的最大容量为`target = sum(stones) // 2`，每件物品的价值和重量都是`stones[i]`，背包容量为`j`时使用前`i`个物品的最大价值记录在二维数组`dp[i][j]`中。这样结束递推后背包中的最大价值为`dp[-1][-1]`，它表示将`stones`分成两个和尽可能相等的子集后其中较小的子集和。此时的返回值为`sum(stones) - 2*dp[-1][-1]`。

[题目链接](https://leetcode.cn/problems/last-stone-weight-ii/)：

```python
class Solution:
    def lastStoneWeightII(self, stones: List[int]) -> int:
        N = len(stones)
        target = sum(stones) // 2

        dp = [[0 for j in range(target+1)] for i in range(N)]

        for j in range(target+1):
            if j >= stones[0]:
                dp[0][j] = stones[0]

        for i in range(1, N):
            for j in range(1, target+1):
                if j >= stones[i]:
                    dp[i][j] = max(dp[i-1][j], dp[i-1][j - stones[i]]+stones[i])
                else:
                    dp[i][j] = dp[i-1][j]
        
        return sum(stones) - 2*dp[-1][-1]
```
{: .snippet}

本题的一维数组递推代码可参考如下。

[题目链接](https://leetcode.cn/problems/last-stone-weight-ii/)：

```python
class Solution:
    def lastStoneWeightII(self, stones: List[int]) -> int:
        N = len(stones)
        target = sum(stones) // 2

        dp = [0 for j in range(target+1)]

        for i in range(N):
            for j in range(target, stones[i]-1,-1):
                dp[j] = max(dp[j], dp[j - stones[i]] + stones[i])
        
        return sum(stones) - 2*dp[-1]
```
{: .snippet}

### 494. 目标和

给你一个整数数组`nums`和一个整数`target`。

向数组中的每个整数前添加`'+'`或`'-'`，然后串联起所有整数，可以构造一个**表达式**：

- 例如，`nums = [2, 1]`，可以在`2`之前添加`'+'`，在`1`之前添加`'-'`，然后串联起来得到表达式`"+2-1"`。

返回可以通过上述方法构造的、运算结果等于`target`的不同**表达式**的数目。

**示例1：**

```
输入：nums = [1,1,1,1,1], target = 3
输出：5
解释：一共有 5 种方法让最终目标和为 3 。
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3
```

**示例2：**

```
输入：nums = [1], target = 1
输出：1
```

**提示：**

- 1 <= `nums.length` <= 20
- 0 <= `nums[i]` <= 1000
- 0 <= `sum(nums[i])` <= 1000
- -1000 <= `target` <= 1000

#### Solution

本题中我们需要把`nums`中的元素分为两组，其中正数部分的和为`pos`而负数部分的和为`neg`，且它们满足：

- `pos + neg = sum(nums)`
- `pos - neg = target`

这样我们就可以求出`pos = (target + sum(nums)) // 2`。此时本题就转换为在`nums`中选择一个子集使其和为`pos`，而我们的目标则是找到这样的子集的数目。

实际上这样的问题可以看成是01背包问题的一种变体。我们建立一个二维数组`dp[][]`，它有`N+1`行`pos+1`列。其中元素`dp[i+1][j]`表示数组中前`i`个元素和为`j`的子集数目，这样可以得到递推关系：

- `dp[i+1][j] = dp[i][j] + dp[i][j - nums[i]]`

在进行初始化时我们需要令`dp[0][0] = 1`，它表示没有任何元素选中时空集的和恰为`0`，因此只存在这一种子集满足要求。接下来就只需要完成递推并返回`dp[-1][-1]`即可。

[题目链接](https://leetcode.cn/problems/target-sum/)：

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        sumNums = sum(nums)

        if abs(target) > sumNums or (sumNums + target) % 2:
            return 0
        
        pos = (sumNums + target) // 2

        N = len(nums)
        dp = [[0 for j in range(pos+1)] for i in range(N+1)]
        dp[0][0] = 1

        for i in range(1, N+1):
            num = nums[i-1]
            for j in range(pos+1):
                dp[i][j] = dp[i-1][j]

                if j >= num:
                    dp[i][j] += dp[i-1][j-num]

        return dp[-1][-1]
```
{: .snippet}

本题的一维数组递推代码可参考如下。

[题目链接](https://leetcode.cn/problems/target-sum/)：

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        sumNums = sum(nums)

        if abs(target) > sumNums or (sumNums + target) % 2:
            return 0
        
        pos = (sumNums + target) // 2

        N = len(nums)
        dp = [0 for j in range(pos+1)]
        dp[0] = 1

        for i in range(N):
            for j in range(pos, nums[i] - 1, -1):
                dp[j] += dp[j - nums[i]]

        return dp[-1]
```
{: .snippet}

### 474. 一和零

给你一个二进制字符串数组`strs`和两个整数`m`和`n`。

请你找出并返回`strs`的最大子集的长度，该子集中**最多**有`m`个`0`和`n`个`1`。

如果`x`的所有元素也是`y`的元素，集合`x`是集合`y`的**子集**。

**示例1：**

```
输入：strs = ["10", "0001", "111001", "1", "0"], m = 5, n = 3
输出：4
解释：最多有 5 个 0 和 3 个 1 的最大子集是 {"10","0001","1","0"} ，因此答案是 4 。
其他满足题意但较小的子集包括 {"0001","1"} 和 {"10","1","0"} 。{"111001"} 不满足题意，因为它含 4 个 1 ，大于 n 的值 3 。
```

**示例2：**

```
输入：strs = ["10", "0", "1"], m = 1, n = 1
输出：2
解释：最大的子集是 {"0", "1"} ，所以答案是 2 。
```

**提示：**

- 1 <= `strs.length` <= 600
- 1 <= `strs[i].length` <= 100
- `strs[i]`仅由`'0'`和`'1'`组成
- 1 <= `m`, `n` <= 100

#### Solution

本题中我们需要建立一个三维`dp[][][]`数组来进行递推。`dp[i+1][j][k]`表示使用前`i`个字符串能够得到的最多包含`j`个`0`和`k`个`1`的子集大小，显然这样的`dp[][][]`数组可以把每个元素都初始化为`0`。接下来考虑递推关系，对于第`i`个字符串有两种可能性：

1. 第`i`个字符串不在满足要求的子集中，此时`dp[i+1][j][k] = dp[i][j][k]`
2. 第`i`个字符串在满足要求的子集中，此时`dp[i+1][j][k] = dp[i][j-zeros][k-ones]+1`，其中`zeros`和`ones`分别为第`i`个字符串中的`0`和`1`数量

这样我们就需要对以上两种情况取最大值，得到递推关系：

- `dp[i+1][j][k] = max(dp[i][j][k], dp[i][j-zeros][k-ones]+1)`

然后通过三重循环进行递推即可。

[题目链接](https://leetcode.cn/problems/ones-and-zeroes/)：

```python
class Solution:
    def findMaxForm(self, strs: List[str], m: int, n: int) -> int:
        N = len(strs)

        dp = [[[0 for k in range(n+1)] for j in range(m+1)]for i in range(N+1)]

        for i in range(1, N+1):
            zeros= strs[i-1].count("0")
            ones = strs[i-1].count("1")

            for j in range(m+1):
                for k in range(n+1):
                    dp[i][j][k] = dp[i-1][j][k]

                    if j >= zeros and k >= ones:
                        dp[i][j][k] = max(dp[i][j][k], dp[i-1][j-zeros][k-ones]+1)
        
        return dp[-1][-1][-1]
```
{: .snippet}

本题的二维数组递推代码可参考如下。

[题目链接](https://leetcode.cn/problems/ones-and-zeroes/)：

```python
class Solution:
    def findMaxForm(self, strs: List[str], m: int, n: int) -> int:
        N = len(strs)

        dp = [[0 for k in range(n+1)] for j in range(m+1)]

        for i in range(N):
            zeros= strs[i].count("0")
            ones = strs[i].count("1")

            for j in range(m, zeros-1, -1):
                for k in range(n, ones-1, -1):
                    dp[j][k] = max(dp[j][k], dp[j-zeros][k-ones]+1)
        
        return dp[-1][-1]
```
{: .snippet}

## 打家劫舍

## 股票问题

## 子序列问题

## Reference

- [动态规划理论基础](https://www.bilibili.com/video/BV13Q4y197Wg/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：509.斐波那契数](https://www.bilibili.com/video/BV1f5411K7mo/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：70.爬楼梯](https://www.bilibili.com/video/BV17h411h7UH/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：746.使用最小花费爬楼梯](https://www.bilibili.com/video/BV16G411c7yZ/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：62.不同路径](https://www.bilibili.com/video/BV1ve4y1x7Eu/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：63.不同路径 II](https://www.bilibili.com/video/BV1Ld4y1k7c6/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：343.整数拆分](https://www.bilibili.com/video/BV1Mg411q7YJ/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：96.不同的二叉搜索树](https://www.bilibili.com/video/BV1eK411o7QA/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [01背包理论基础](https://www.bilibili.com/video/BV1cg411g7Y6/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [01背包理论基础(滚动数组)](https://www.bilibili.com/video/BV1BU4y177kY/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：416.分割等和子集](https://www.bilibili.com/video/BV1rt4y1N7jE/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：1049.最后一块石头的重量II](https://www.bilibili.com/video/BV14M411C7oV/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：494.目标和](https://www.bilibili.com/video/BV1o8411j73x/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：474.一和零](https://www.bilibili.com/video/BV1rW4y1x7ZQ/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
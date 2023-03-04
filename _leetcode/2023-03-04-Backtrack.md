---
layout: article
title: 回溯
key: leetcode-08
clipboard: true
aside:
  toc: true
sidebar:
  nav: LeetCode
---

## 组合

### 77. 组合

给定两个整数`n`和`k`，返回范围`[1, n]`中所有可能的`k`个数的组合。

你可以按**任何顺序**返回答案。

**示例1：**

```
输入：n = 4, k = 2
输出：
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

**示例2：**

```
输入：n = 1, k = 1
输出：[[1]]
```

**提示：**

- 1 <= `n` <= 20。
- 1 <= `k` <= `n`。

#### Solution

[题目链接](https://leetcode.cn/problems/combinations/)：

```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
```
{: .snippet}

## Reference

- [二叉树理论基础](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)
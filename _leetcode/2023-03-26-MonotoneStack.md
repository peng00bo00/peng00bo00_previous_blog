---
layout: article
title: 单调栈
key: leetcode-11
clipboard: true
aside:
  toc: true
sidebar:
  nav: LeetCode
---

**单调栈(monotone stack)**是一种特殊的栈。在栈**先进先出**的基础上，单调栈要求栈中的元素按照从栈顶到栈底的顺序是**单调递增**或是**单调递减**，因此单调栈适合求解"第一个大于"或"第一个小于"某个元素这样的问题。

<div align=center>
<img src="https://images.weserv.nl/?url=i.imgur.com/qYBAlZK.png" width="80%">
</div>

以单调递增栈为例，算法模板可参考如下：

```python
for i in range(len(nums))
    while stack and nums[i] > nums[stack[-1]]:
        idx = stack.pop()
        res[idx] = i - idx
    
    stack.append(i)
```

## 单调递增栈

### 739. 每日温度

给定一个整数数组`temperatures`，表示每天的温度，返回一个数组`answer`，其中`answer[i]`是指对于第`i`天，下一个更高温度出现在几天后。如果气温在这之后都不会升高，请在该位置用`0`来代替。

**示例1：**

```
输入: temperatures = [73,74,75,71,69,72,76,73]
输出: [1,1,4,2,1,1,0,0]
```

**示例2：**

```
输入: temperatures = [30,40,50,60]
输出: [1,1,1,0]
```

**示例3：**

```
输入: temperatures = [30,60,90]
输出: [1,1,0]
```

**提示：**

- 1 <= `temperatures.length` <= 10⁵
- 30 <= `temperatures[i]` <= 100

#### Solution

本题是经典的单调递增栈问题，它的本质是求数组中大于当前元素的第一个元素编号。这里我们使用一个栈`stack`作为单调递增栈保存每一天的编号，使用数组`answer`记录结果。当我们对`temperatures`进行遍历时令当前编号`i`入栈，根据单调栈的性质所有小于`temperatures[i]`的编号`idx`会依次出栈。因此`i`即为`idx`后出现的第一个大于它的数字编号，它们之间的距离为`answer[idx] = i-idx`。由于`temperatures`中所有的元素只会入栈一次，使用单调栈的时间复杂度为`O(n)`。

[题目链接](https://leetcode.cn/problems/daily-temperatures/)：

```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        N = len(temperatures)
        answer = [0 for i in range(N)]
        stack = []

        for i in range(N):
            while stack and temperatures[i] > temperatures[stack[-1]]:
                idx = stack.pop()
                answer[idx] = i - idx
            
            stack.append(i)

        return answer
```
{: .snippet}

## 单调递减栈

## Reference

- [LeetCode：739.每日温度](https://www.bilibili.com/video/BV1my4y1Z7jj/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
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

### 496. 下一个更大元素 I

`nums1`中数字`x`的**下一个更大元素**是指`x`在`nums2`中对应位置**右侧**的**第一个**比`x`大的元素。

给你两个**没有重复元素**的数组`nums1`和`nums2`，下标从`0`开始计数，其中`nums1`是`nums2`的子集。

对于每个`0 <= i < nums1.length`，找出满足`nums1[i] == nums2[j]`的下标`j`，并且在`nums2`确定`nums2[j]`的**下一个更大元素**。如果不存在下一个更大元素，那么本次查询的答案是`-1`。

返回一个长度为`nums1.length`的数组`ans`作为答案，满足`ans[i]`是如上所述的**下一个更大元素**。

**示例1：**

```
输入：nums1 = [4,1,2], nums2 = [1,3,4,2].
输出：[-1,3,-1]
解释：nums1 中每个值的下一个更大元素如下所述：
- 4 ，用加粗斜体标识，nums2 = [1,3,4,2]。不存在下一个更大元素，所以答案是 -1 。
- 1 ，用加粗斜体标识，nums2 = [1,3,4,2]。下一个更大元素是 3 。
- 2 ，用加粗斜体标识，nums2 = [1,3,4,2]。不存在下一个更大元素，所以答案是 -1 。
```

**示例2：**

```
输入：nums1 = [2,4], nums2 = [1,2,3,4].
输出：[3,-1]
解释：nums1 中每个值的下一个更大元素如下所述：
- 2 ，用加粗斜体标识，nums2 = [1,2,3,4]。下一个更大元素是 3 。
- 4 ，用加粗斜体标识，nums2 = [1,2,3,4]。不存在下一个更大元素，所以答案是 -1 。
```

**提示：**

- 1 <= `nums1.length` <= `nums2.length` <= 1000
- 0 <= `nums1[i]`, `nums2[i]` <= 10⁴
- `nums1`和`nums2`中所有整数**互不相同**
- `nums1`中的所有整数同样出现在`nums2`中

#### Solution

由于`nums1`和`nums2`中所有整数互不相同且`nums1`是`nums2`的子集，本题可以理解为寻找`nums2`中每个元素右边第一个大于它的值。这里使用`stack`作为单调递增栈，`ans`作为字典(哈希表)记录`nums2`中元素的下一个更大元素。

使用单调栈时需要注意**从右向左**对`nums2`进行遍历，如果当前元素`num`大于栈顶元素`stack[-1]`则令其出栈。这样在`num`入栈前如果存在`stack[-1]`则其就是`num`对应的下一个更大元素，令`ans[num] = stack[-1]`；否则说明`num`右侧元素都小于它，令`ans[num] = -1`。完成对`nums2`的遍历后从`ans`中提取`nums1`中元素对应的下一个更大元素即可。

[题目链接](https://leetcode.cn/problems/next-greater-element-i/)：

```python
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        N = len(nums2)

        stack = []
        ans = {}

        for i in range(N-1, -1, -1):
            num = nums2[i]
            while stack and num > stack[-1]:
                stack.pop()
            
            ans[num] = stack[-1] if stack else -1
            stack.append(num)
        
        return [ans[num] for num in nums1]
```
{: .snippet}

## 单调递减栈

## Reference

- [LeetCode：739.每日温度](https://www.bilibili.com/video/BV1my4y1Z7jj/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：496.下一个更大元素 I](https://www.bilibili.com/video/BV1jA411m7dX/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
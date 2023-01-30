---
layout: article
title: 双指针
key: leetcode-05
clipboard: true
aside:
  toc: true
sidebar:
  nav: LeetCode
---

## 数组

### 27. 移除元素

同[27. 移除元素](/leetcode/2023-01-02-Array.html#27-移除元素)。

#### Solution

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        fast, slow = 0, 0

        for fast in range(len(nums)):
            if nums[fast] != val:
                nums[slow] = nums[fast]
                slow += 1

        return slow
```
{: .snippet}

## 字符串

## 链表

## Reference


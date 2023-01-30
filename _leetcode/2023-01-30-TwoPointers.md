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

[题目链接](https://leetcode.cn/problems/remove-element/)：

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

### 344. 反转字符串

同[344. 反转字符串](/leetcode/2023-01-23-String.html#344-反转字符串)。

#### Solution

[题目链接](https://leetcode.cn/problems/reverse-string/)：

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """

        left, right = 0, len(s)-1

        while left < right:
            s[left], s[right] = s[right], s[left]

            left += 1
            right-= 1
```
{: .snippet}

### 剑指Offer 05.替换空格

同[剑指Offer 05.替换空格](/leetcode/2023-01-23-String.html#剑指offer-05替换空格)。

#### Solution

[题目链接](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)：

```python
class Solution:
    def replaceSpace(self, s: str) -> str:
        N = len(s)

        for i, char in enumerate(s[::-1]):
            if char == " ":
                s = s[:N-(i+1)] + "%20" + s[N-i:]
        
        return s
```
{: .snippet}

### 151. 反转字符串中的单词

同[151. 反转字符串中的单词](/leetcode/2023-01-23-String.html#151-反转字符串中的单词)。

#### Solution

[题目链接](https://leetcode.cn/problems/reverse-words-in-a-string/)：

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        def removeSpace(s_list: List[str]) -> List[str]:
            left, right = 0, len(s_list)-1

            while s_list[left] == " ":
                left += 1
            
            while s_list[right] == " ":
                right -= 1
            
            ret = []

            while left <= right:
                if s_list[left] != " ":
                    ret.append(s_list[left])
                    left += 1
                else:
                    while s_list[left] == " ":
                        left += 1

                    ret.append(" ")

            return ret
        
        def reverse(s_list: List[str]) -> List[str]:
            left, right = 0, len(s_list)-1

            while left < right:
                s_list[left], s_list[right] = s_list[right], s_list[left]

                left += 1
                right-= 1

            return s_list

        s_list = list(s)

        ## remove extra spaces
        s_list = removeSpace(s_list)

        ## reverse the whole string
        s_list = reverse(s_list)

        ## reverse each word
        fast, slow = 0, 0
        s_list.append(" ")

        for fast in range(len(s_list)):
            if s_list[fast] != " ":
                continue
            
            s_list[slow: fast] = reverse(s_list[slow: fast])

            slow = fast+1

        s_list.pop()

        return "".join(s_list)
```
{: .snippet}

## 链表

## Reference

- [LeetCode：27. 移除元素](https://www.bilibili.com/video/BV12A4y1Z7LP/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：344. 反转字符串](https://www.bilibili.com/video/BV1fV4y17748/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：151. 翻转字符串里的单词](https://www.bilibili.com/video/BV1uT41177fX/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
---
layout: article
title: 哈希表
key: leetcode-03
clipboard: true
aside:
  toc: true
sidebar:
  nav: LeetCode
---

## 比较数组/字符串

### 242. 有效的字母异位词

给定两个字符串`s`和`t`，编写一个函数来判断`t`是否是`s`的字母异位词。

**注意**：若`s`和`t`中每个字符出现的次数都相同，则称`s`和`t`互为字母异位词。

**示例1：**

```
输入: s = "anagram", t = "nagaram"
输出: true
```

**示例2：**

```
输入: s = "rat", t = "car"
输出: false
```

**提示：**

- 1 <= `s.length, t.length` <= 5 * 10⁴。
- `s`和`t`仅包含小写字母。

#### Solution

[题目链接](https://leetcode.cn/problems/valid-anagram/)：

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        
        s_dict = {}
        t_dict = {}

        for char in s:
            s_dict[char] = s_dict.get(char, 0) + 1
        
        for char in t:
            t_dict[char] = t_dict.get(char, 0) + 1
        
        for char in s_dict.keys():
            if s_dict[char] != t_dict.get(char, 0):
                return False
        
        for char in t_dict.keys():
            if t_dict[char] != s_dict.get(char, 0):
                return False

        return True
```
{: .snippet}

```python
class Solution(object):
    def isAnagram(self, s: str, t: str) -> bool:
        from collections import Counter

        a_count = Counter(s)
        b_count = Counter(t)
        
        return a_count == b_count
```
{: .snippet}

## 公共元素



## Reference

- [哈希表理论基础](https://programmercarl.com/%E9%93%BE%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)
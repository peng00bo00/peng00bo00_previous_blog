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

### 202. 快乐数

编写一个算法来判断一个数`n`是不是快乐数。

**「快乐数」**定义为：

- 对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和。
- 然后重复这个过程直到这个数变为`1`，也可能是**无限循环**但始终变不到`1`。
- 如果这个过程**结果**为`1`，那么这个数就是快乐数。

如果`n`是*快乐数*就返回`true`；不是，则返回`false`。

**示例1：**

```
输入：n = 19
输出：true
解释：
1² + 9² = 82
8² + 2² = 68
6² + 8² = 100
1² + 0² + 0² = 1
```

**示例2：**

```
输入：n = 2
输出：false
```

**提示：**

- 1 <= `n` <= 2<sup>31</sup> - 1。

#### Solution

[题目链接](https://leetcode.cn/problems/happy-number/)：

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        def nextHappy(x):
            xx = 0
            while x > 0:
                xx += (x % 10)**2
                x = x // 10
            
            return xx
        
        record = {}
        while True:
            n = nextHappy(n)

            if n == 1:
                return True
            
            record[n] = record.get(n, 0) + 1
            if record[n] > 1:
                return False
```
{: .snippet}

### 1. 两数之和

给定一个整数数组`nums`和一个整数目标值`target`，请你在该数组中找出**和为目标值**`target`的那**两个**整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

**示例 1：**

```
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

**示例 2：**

```
输入：nums = [3,2,4], target = 6
输出：[1,2]
```

**示例 3：**

```
输入：nums = [3,3], target = 6
输出：[0,1]
```

**提示：**

- 2 <= `nums.length` <= 10⁴。
- -10⁹ <= `nums[i]` <= 10⁹。
- -10⁹ <= `target` <= 10⁹。
- **只会存在一个有效答案**。

#### Solution

[题目链接](https://leetcode.cn/problems/two-sum/)：

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        records = {}
        for idx, num in enumerate(nums):
            if target-num in records:
                return [idx, records[target-num]]
            
            records[num] = idx
        
        return []
```
{: .snippet}

## 公共元素

### 1002. 查找共用字符

给你一个字符串数组`words`，请你找出所有在`words`的每个字符串中都出现的共用字符(**包括重复字符**)，并以数组形式返回。你可以按**任意顺序**返回答案。

**示例1：**

```
输入：words = ["bella","label","roller"]
输出：["e","l","l"]
```

**示例2：**

```
输入：words = ["cool","lock","cook"]
输出：["c","o"]
```

**提示：**

- 1 <= `words.length` <= 100。
- 1 <= `words[i].length` <= 100。
- `words[i]`由小写英文字母组成。

#### Solution

[题目链接](https://leetcode.cn/problems/find-common-characters/)：

```python
class Solution:
    def commonChars(self, words: List[str]) -> List[str]:
        minfreq = [float("inf")] * 26
        for word in words:
            freq = [0] * 26
            for ch in word:
                freq[ord(ch) - ord("a")] += 1
            for i in range(26):
                minfreq[i] = min(minfreq[i], freq[i])
        
        ans = list()
        for i in range(26):
            ans.extend([chr(i + ord("a"))] * minfreq[i])

        return ans
```
{: .snippet}

```python
class Solution:
    def commonChars(self, words: List[str]) -> List[str]:
        tmp = collections.Counter(words[0])
        l = []
        for i in range(1,len(words)):
            # 使用 & 取交集
            tmp = tmp & collections.Counter(words[i])

        # 剩下的就是每个单词都出现的字符（键），个数（值）
        for j in tmp:
            v = tmp[j]
            while(v):
                l.append(j)
                v -= 1
        return l
```
{: .snippet}

### 349. 两个数组的交集

给定两个数组`nums1`和`nums2`，返回**它们的交集**。输出结果中的每个元素一定是**唯一**的。我们可以**不考虑输出结果的顺序**。

**示例1：**

```
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2]
```

**示例2：**

```
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[9,4]
解释：[4,9] 也是可通过的
```

**提示：**

- 1 <= `nums1.length, nums2.length` <= 1000。
- 0 <= `nums1[i], nums2[i]` <= 1000。

#### Solution

[题目链接](https://leetcode.cn/problems/intersection-of-two-arrays/)：

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        set1 = {num: 1 for num in nums1}
        set2 = {num: 1 for num in nums2}

        return [num for num in set1 if num in set2]
```
{: .snippet}

## Reference

- [哈希表理论基础](https://programmercarl.com/%E5%93%88%E5%B8%8C%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)
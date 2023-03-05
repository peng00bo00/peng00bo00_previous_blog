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

**回溯(backtracking)**的本质是暴力搜索，一般会通过函数的递归来实现。回溯一般可以解决如下问题：

- 组合问题：N个数里面按一定规则找出k个数的集合
- 切割问题：一个字符串按一定规则有几种切割方式
- 子集问题：一个N个数的集合里有多少符合条件的子集
- 排列问题：N个数按一定规则全排列，有几种排列方式
- 棋盘问题：N皇后，解数独等

所有回溯可以解决的问题都可以抽象为树的结构。每一步问题子集的大小定义了树的宽度，而递归的次数定义了树的深度。

<div align=center>
<img src="https://images.weserv.nl/?url=i.imgur.com/OlMp0Bz.png" width="80%">
</div>

回溯的算法模板大致如下：

```
def backtracking():
    if 终止条件:
        存放结果
        return
    
    for (选择：本层集合中元素 (树中节点孩子的数量就是集合的大小) ):
        处理节点
        递归 backtracking()
        回溯(撤销对节点的处理)
```

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

组合问题是回溯算法的经典应用。由于组合是无序的，我们引入一个变量`startIdx`表示本次(递归)调用开始的数字，即本次递归中处理的子集为`[startIdx, startIdx+1, ..., n]`，这样就可以保证每次递归的结果不会和前面出现重复。

<div align=center>
<img src="https://images.weserv.nl/?url=i.imgur.com/LEDr8Cj.png" width="80%">
</div>

[题目链接](https://leetcode.cn/problems/combinations/)：

```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        res  = []
        path = []

        def backtracking(n: int, k: int, startIdx: int) -> None:
            if len(path) == k:
                res.append(path[:])
                return
            
            for i in range(startIdx, n+1):
                path.append(i)
                backtracking(n, k, i+1)
                path.pop()
        
        backtracking(n, k, 1)

        return res
```
{: .snippet}

更进一步，我们可以利用当前路径`path`的长度来控制每一层循环次数。假设当前搜索过程的路径为`path`而起始数字为`startIdx`，那么本层for循环中可能的最大数字为`n - (k - len(path)) + 1`，当`i`超过这个数字时集合中的剩余元素就小于`k`也就无法形成有效的`path`。利用这一性质我们可以实现对搜索树的剪枝，从而提升算法效率。剪枝过程可以参考下图。

<div align=center>
<img src="https://images.weserv.nl/?url=i.imgur.com/KGgRln1.png" width="90%">
</div>

使用剪枝来优化后的代码可参考如下。

[题目链接](https://leetcode.cn/problems/combinations/)：

```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        res  = []
        path = []

        def backtracking(n: int, k: int, startIdx: int) -> None:
            if len(path) == k:
                res.append(path[:])
                return
            
            for i in range(startIdx, n-(k-len(path))+2):
                path.append(i)
                backtracking(n, k, i+1)
                path.pop()
        
        backtracking(n, k, 1)

        return res
```
{: .snippet}

### 216. 组合总和 III

找出所有相加之和为`n`的`k`个数的组合，且满足下列条件：

- 只使用数字1到9
- 每个数字**最多使用一次**

返回**所有可能的有效组合的列表**。该列表不能包含相同的组合两次，组合可以以任何顺序返回。

**示例1：**

```
输入: k = 3, n = 7
输出: [[1,2,4]]
解释:
1 + 2 + 4 = 7
没有其他符合的组合了。
```

**示例2：**

```
输入: k = 3, n = 9
输出: [[1,2,6], [1,3,5], [2,3,4]]
解释:
1 + 2 + 6 = 9
1 + 3 + 5 = 9
2 + 3 + 4 = 9
没有其他符合的组合了。
```

**示例3：**

```
输入: k = 4, n = 1
输出: []
解释: 不存在有效的组合。
在[1,9]范围内使用4个不同的数字，我们可以得到的最小和是1+2+3+4 = 10，因为10 > 1，没有有效的组合。
```

**提示：**

- 2 <= `k` <= 9。
- 1 <= `n` <= `60`。

#### Solution

本题的暴力解法类似于[组合](/leetcode/2023-03-04-Backtracking.html#77-组合)，我们只需要在收集结果时要求总和为`n`即可。

[题目链接](https://leetcode.cn/problems/combination-sum-iii/)：

```python
class Solution:
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        res = []
        path= []

        def backtracking(n, k, startIdx):
            if len(path) == k and sum(path) == n:
                res.append(path[:])
                return
            
            for i in range(startIdx, 10):
                path.append(i)
                backtracking(n, k, i+1)
                path.pop()
        
        backtracking(n, k, 1)

        return res
```
{: .snippet}

本题的剪枝过程类似于[组合](/leetcode/2023-03-04-Backtracking.html#77-组合)，即每次for循环时数字的最大值为`10 - (k - len(path))`。除此之外我们还可以记录下当前`path`中数字的和`s = sum(path)`，当`s > n`时提前结束搜索。

<div align=center>
<img src="https://images.weserv.nl/?url=i.imgur.com/kM7Sby1.png">
</div>

[题目链接](https://leetcode.cn/problems/combination-sum-iii/)：

```python
class Solution:
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        res = []
        path= []

        def backtracking(n: int, k: int, startIdx: int, s: int) -> None:
            if s > n:
                return
            
            if len(path) == k:
                if s == n:
                    res.append(path[:])
                return
            
            for i in range(startIdx, 10 - (k - len(path)) + 1):
                path.append(i)
                backtracking(n, k, i+1, s+i)
                path.pop()
        
        backtracking(n, k, 1, 0)

        return res
```
{: .snippet}

### 17. 电话号码的字母组合

给定一个仅包含数字`2-9`的字符串，返回所有它能表示的字母组合。答案可以按**任意顺序**返回。

给出数字到字母的映射如下(与电话按键相同)。注意`1`不对应任何字母。

<div align=center>
<img src="https://images.weserv.nl/?url=assets.leetcode-cn.com/aliyun-lc-upload/uploads/2021/11/09/200px-telephone-keypad2svg.png">
</div>

**示例1：**

```
输入：digits = "23"
输出：["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

**示例2：**

```
输入：digits = ""
输出：[]
```

**示例3：**

```
输入：digits = "2"
输出：["a","b","c"]
```

**提示：**

- 0 <= `digits.length` <= 4。
- `digits[i]`是范围`['2', '9']`的一个数字。

#### Solution

本题的暴力解法类似于[组合](/leetcode/2023-03-04-Backtracking.html#77-组合)，在处理时需要先建立数字到字母的映射`keyboard`然后对所有可能的字母组合进行暴力搜索。

<div align=center>
<img src="https://images.weserv.nl/?url=i.imgur.com/gee7c8t.png" width="80%">
</div>

[题目链接](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/)：

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        keyboard = {
            "2": "abc",
            "3": "def",
            "4": "ghi",
            "5": "jkl",
            "6": "mno",
            "7": "pqrs",
            "8": "tuv",
            "9": "wxyz"
        }

        res = []
        path= []

        def backtracking(idx: int) -> None:
            if idx == len(digits):
                if path:
                    res.append("".join(path[:]))
                return
            
            number = digits[idx]
            for letter in keyboard[number]:
                path.append(letter)
                backtracking(idx+1)
                path.pop()
        
        backtracking(0)

        return res
```
{: .snippet}

### 39. 组合总和

给你一个**无重复元素**的整数数组`candidates`和一个目标整数`target`，找出`candidates`中可以使数字和为目标数`target`的所有**不同组合**，并以列表形式返回。你可以按**任意顺序**返回这些组合。

`candidates`中的**同一个**数字可以**无限制重复被选取**。如果至少一个数字的被选数量不同，则两种组合是不同的。

对于给定的输入，保证和为`target`的不同组合数少于`150`个。

**示例1：**

```
输入：candidates = [2,3,6,7], target = 7
输出：[[2,2,3],[7]]
解释：
2 和 3 可以形成一组候选，2 + 2 + 3 = 7 。注意 2 可以使用多次。
7 也是一个候选， 7 = 7 。
仅有这两种组合。
```

**示例2：**

```
输入: candidates = [2,3,5], target = 8
输出: [[2,2,2,2],[2,3,3],[3,5]]
```

**示例3：**

```
输入: candidates = [2], target = 1
输出: []
```

**提示：**

- 1 <= `candidates.length` <= 30。
- 2 <= `candidates[i]` <= 40。
- `candidates`的所有元素**互不相同**。
- 1 <= `target` <= 40。

#### Solution

本题解法类似于[组合总和 III](/leetcode/2023-03-04-Backtracking.html#216-组合总和-iii)，我们需要使用`startIdx`来记录当前搜索的起始数字索引，再使用`s`来记录搜索路径上的数字之和。和[组合总和 III](/leetcode/2023-03-04-Backtracking.html#216-组合总和-iii)不同的是本题中允许数字的重复使用，因此在进行回溯时不会修改当前的子集大小而是利用`s`和`target`的大小关系来控制递归是否终止。整个算法过程可以参考如下。

<div align=center>
<img src="https://images.weserv.nl/?url=i.imgur.com/JQ1lTUf.png" width="90%">
</div>

[题目链接](https://leetcode.cn/problems/combination-sum/)：

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []
        path= []

        def backtracking(startIdx: int, s: int) -> None:
            if s > target:
                return
            elif s == target:
                res.append(path[:])
                return
            
            for i in range(startIdx, len(candidates)):
                num = candidates[i]

                path.append(num)
                backtracking(i, s+num)
                path.pop()
        
        backtracking(0, 0)

        return res
```
{: .snippet}

而在进行剪枝优化时则需要先对`candidates`数组进行排序。然后在每一层的循环中如果发现`s+num > target`则表明之后的每一次循环`s+num`都会大于`target`，因此我们可以提前终止循环。

<div align=center>
<img src="https://images.weserv.nl/?url=i.imgur.com/S1aCkUV.png" width="90%">
</div>

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []
        path= []
        
        candidates = sorted(candidates)

        def backtracking(startIdx: int, s: int) -> None:

            if s == target:
                res.append(path[:])
                return
            
            for i in range(startIdx, len(candidates)):
                num = candidates[i]

                if s+num > target:
                    return

                path.append(num)
                backtracking(i, s+num)
                path.pop()
        
        backtracking(0, 0)

        return res
```
{: .snippet}

### 40. 组合总和 II

给定一个候选人编号的集合`candidates`和一个目标数`target`，找出`candidates`中所有可以使数字和为`target`的组合。

`candidates`中的每个数字在每个组合中只能使用**一次**。

**注意：**解集不能包含重复的组合。 

**示例1：**

```
输入: candidates = [10,1,2,7,6,1,5], target = 8,
输出:
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```

**示例2：**

```
输入: candidates = [2,5,2,1,2], target = 5,
输出:
[
[1,2,2],
[5]
]
```

**提示：**

- 1 <= `candidates.length` <= 100。
- 1 <= `candidates[i]` <= 50。
- 1 <= `target` <= 30。

#### Solution

本题和[组合总和](/leetcode/2023-03-04-Backtracking.html#39-组合总和)的区别在于`candidates`中的每个数字只能使用一次，而且`candidates`中可能会出现重复的数字。因此本题的关键在于如何对`candidates`进行去重，即保证使用过的元素不会被重复选取。这里可以首先对`candidates`进行**排序**，然后在进行循环时保证每个起始数字只会进行一次递归搜索。

[题目链接](https://leetcode.cn/problems/combination-sum/)：

```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []
        path= []
        candidates = sorted(candidates)

        def backtracking(startIdx: int, s: int) -> None:
            if s == target:
                res.append(path[:])
                return
            
            for i in range(startIdx, len(candidates)):
                num = candidates[i]

                if s+num > target:
                    return
                
                ## skip used num
                if i > startIdx and num == candidates[i-1]:
                    continue

                path.append(num)
                backtracking(i+1, s+num)
                path.pop()
        
        backtracking(0, 0)

        return res
```
{: .snippet}

## Reference

- [回溯算法理论基础](https://www.bilibili.com/video/BV1cy4y167mM/?vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：77.组合](https://www.bilibili.com/video/BV1ti4y1L7cv/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：77.组合(剪枝)](https://www.bilibili.com/video/BV1wi4y157er/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：216.组合总和III](https://www.bilibili.com/video/BV1wg411873x/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：17.电话号码的字母组合](https://www.bilibili.com/video/BV1yV4y1V7Ug/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：39.组合总和](https://www.bilibili.com/video/BV1KT4y1M7HJ/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：40.组合总和II](https://www.bilibili.com/video/BV12V4y1V73A/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
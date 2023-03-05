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

## Reference

- [回溯算法理论基础](https://www.bilibili.com/video/BV1cy4y167mM/?vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：77.组合](https://www.bilibili.com/video/BV1ti4y1L7cv/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：77.组合(剪枝)](https://www.bilibili.com/video/BV1wi4y157er/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：216.组合总和III](https://www.bilibili.com/video/BV1wg411873x/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：17.电话号码的字母组合](https://www.bilibili.com/video/BV1yV4y1V7Ug/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
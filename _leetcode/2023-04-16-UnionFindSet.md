---
layout: article
title: 并查集
key: leetcode-13
clipboard: true
aside:
  toc: true
sidebar:
  nav: LeetCode
---

**并查集(union-find set)**是一种用于管理元素所属集合的数据结构。它的实现为一个森林，其中每棵树表示一个集合，树中的节点表示对应集合中的元素。

<div align=center>
<img src="https://images.weserv.nl/?url=he-s3.s3.amazonaws.com/media/uploads/4c11a99.jpg" width="60%">
<img src="https://images.weserv.nl/?url=he-s3.s3.amazonaws.com/media/uploads/7439d01.jpg" width="60%">
</div>

并查集需要实现**合并(union)**和**查询(find)**两个操作：

- 合并：合并两个元素所属集合(合并对应的树)
- 查询：查询某个元素所属的集合(树的根节点)，一般可以用来判断两个元素是否来自同一集合

并查集的经典应用在于处理**动态连接(dynamic connectivity)**问题，即判断两个对象是否相互联通或者图上有多少不连通的集合。因此在初始化并查集时我们需要初始化两个属性：`self.pa`用来记录每个节点的父节点，以及`self.count`用来记录图上的集合数。

```python
class UnionFindSet:
    def __init__(self, n: int):
        self.pa    = [i for i in range(n)]  ## 初始化每个节点的父节点为其自身
        self.count = n                      ## 初始化集合数为全部节点数
```

使用并查集进行查询时需要调用`find(x)`方法返回`x`节点的根节点，这里还可以结合**路径压缩**的技巧来加快查询速度。

```python
def find(self, x: int) -> int:
    if self.pa[x] != x:
        self.pa[x] = self.find(self.pa[x])  ## 路径压缩
    
    return self.pa[x]
```

在`find(x)`的基础上我们可以实现`union(x, y)`方法用来合并`x`和`y`两个节点所在集合。

```python
def union(self, x: int, y: int) -> None:
    root_x = self.find(x)                   ## 查询x的根节点
    root_y = self.find(y)                   ## 查询y的根节点

    if root_x != root_y:
        self.pa[root_y] = root_x            ## 当x和y来自不同集合时把y的根节点连到x根节点上
        self.count -= 1                     ## 同时集合数量减1
```

并查集的标准实现可以参考如下。

```python
class UnionFindSet:
    def __init__(self, n: int):
        self.pa    = [i for i in range(n)]
        self.count = n
    
    def union(self, x: int, y: int) -> None:
        root_x = self.find(x)
        root_y = self.find(y)

        if root_x != root_y:
            self.pa[root_y] = root_x
            self.count -= 1
    
    def find(self, x: int) -> int:
        if self.pa[x] != x:
            self.pa[x] = self.find(self.pa[x])
        
        return self.pa[x]
```

## 冗余连接

### 684. 冗余连接

树可以看成是一个连通且**无环**的**无向**图。

给定往一棵`n`个节点(节点值`1`～`n`)的树中添加一条边后的图。添加的边的两个顶点包含在`1`到`n`中间，且这条附加的边不属于树中已存在的边。图的信息记录于长度为`n`的二维数组`edges`，`edges[i] = [ai, bi]`表示图中在`ai`和`bi`之间存在一条边。

请找出一条可以删去的边，删除后可使得剩余部分是一个有着`n`个节点的树。如果有多个答案，则返回数组`edges`中最后出现的边。

**示例1：**

<div align=center>
<img src="https://images.weserv.nl/?url=pic.leetcode-cn.com/1626676174-hOEVUL-image.png">
</div>

```
输入：edges = [[1,2], [1,3], [2,3]]
输出：[2,3]
```

**示例2：**

<div align=center>
<img src="https://images.weserv.nl/?url=pic.leetcode-cn.com/1626676179-kGxcmu-image.png">
</div>

```
输入：edges = [[1,2], [2,3], [3,4], [1,4], [1,5]]
输出：[1,4]
```

**提示：**

- `n` == `edges.length`
- 3 <= `n` <= 1000
- `edges[i].length` == 2
- 1 <= `ai` < `bi` <= `edges.length`
- `ai` != `bi`
- `edges`中无重复元素
- 给定的图是连通的

#### Solution

本题的解法在于对`edges`进行遍历，如果边的两个端点`u`和`v`位于不同集合则将它们合并，否则说明它们已经连接到一起了直接返回即可。

[题目链接](https://leetcode.cn/problems/redundant-connection/)：

```python
class UnionFindSet:
    def __init__(self, n: int):
        self.pa    = [i for i in range(n)]
        self.count = n
    
    def union(self, x, y) -> None:
        root_x = self.find(x)
        root_y = self.find(y)

        if root_x != root_y:
            self.pa[root_y] = root_x
            self.count -= 1
    
    def find(self, x: int) -> int:
        if self.pa[x] != x:
            self.pa[x] = self.find(self.pa[x])
        
        return self.pa[x]

class Solution:
    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:
        n = len(edges)

        UF = UnionFindSet(n+1)

        for u, v in edges:
            if UF.find(u) == UF.find(v):
                return [u, v]
            else:
                UF.union(u, v)
        
        return []
```
{: .snippet}

### 685. 冗余连接 II

在本问题中，有根树指满足以下条件的**有向**图。该树只有一个根节点，所有其他节点都是该根节点的后继。该树除了根节点之外的每一个节点都有且只有一个父节点，而根节点没有父节点。

输入一个有向图，该图由一个有着`n`个节点(节点值不重复，从`1`到`n`)的树及一条附加的有向边构成。附加的边包含在`1`到`n`中的两个不同顶点间，这条附加的边不属于树中已存在的边。

结果图是一个以边组成的二维数组`edges`。每个元素是一对`[uᵢ, vᵢ]`，用以表示**有向**图中连接顶点`uᵢ`和顶点`vᵢ`的边，其中`uᵢ`是`vᵢ`的一个父节点。

返回一条能删除的边，使得剩下的图是有`n`个节点的有根树。若有多个答案，返回最后出现在给定二维数组的答案。

**示例1：**

<div align=center>
<img src="https://images.weserv.nl/?url=assets.leetcode.com/uploads/2020/12/20/graph1.jpg">
</div>

```
输入：edges = [[1,2],[1,3],[2,3]]
输出：[2,3]
```

**示例2：**

<div align=center>
<img src="https://images.weserv.nl/?url=assets.leetcode.com/uploads/2020/12/20/graph2.jpg">
</div>

```
输入：edges = [[1,2],[2,3],[3,4],[4,1],[1,5]]
输出：[4,1]
```

**提示：**

- `n` == `edges.length`
- 3 <= `n` <= 1000
- `edges[i].length` == 2
- 1 <= `uᵢ`, `vᵢ` <= `n`

#### Solution

本题的整体思路类似于[冗余连接](/leetcode/2023-04-16-UnionFindSet.html#684-冗余连接)，我们需要对`edges`进行遍历并尝试构造出树结构。由于整个图上只有一条额外的边，这条边有三种可能性：

1. 这条边破坏了树结构，使得某个节点`v`有两个父节点(如示例1中的`[2, 3]`)
2. 这条边导致图上出现了环(如示例2中的`[4, 1]`)
3. 这条边既破坏了树结构又产生了环

[题目链接](https://leetcode.cn/problems/redundant-connection-ii/)：

```python
class UnionFindSet:
    def __init__(self, n: int):
        self.pa    = [i for i in range(n)]
        self.count = n
    
    def find(self, x: int) -> int:
        if self.pa[x] != x:
            self.pa[x] = self.find(self.pa[x])
        return self.pa[x]
    
    def union(self, x: int, y: int) -> None:
        root_x = self.find(x)
        root_y = self.find(y)

        if root_x != root_y:
            self.pa[root_y] = root_x
            self.count -= 1

class Solution:
    def findRedundantDirectedConnection(self, edges: List[List[int]]) -> List[int]:
        n = len(edges)

        UF     = UnionFindSet(n+1)
        parent = [i for i in range(n+1)]

        conflict = -1
        cycle    = -1

        for i, (u, v) in enumerate(edges):
            if parent[v] == v:
                parent[v] = u

                if UF.find(u) == UF.find(v):
                    cycle = i
                else:
                    UF.union(u, v)
            
            else:
                conflict = i
        
        if conflict < 0:
            return edges[cycle]
        else:
            if cycle < 0:
                return edges[conflict]
            else:
                u, v = edges[conflict]
                return [parent[v], v]
```
{: .snippet}
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

**并查集(union-find set)**是一种用于管理元素所属集合的数据结构，实现为一个森林，其中每棵树表示一个集合，树中的节点表示对应集合中的元素。

<div align=center>
<img src="https://images.weserv.nl/?url=oi-wiki.org/ds/images/disjoint-set.svg" width="30%">
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
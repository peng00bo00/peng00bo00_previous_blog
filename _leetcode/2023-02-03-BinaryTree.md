---
layout: article
title: 二叉树
key: leetcode-07
clipboard: true
aside:
  toc: true
sidebar:
  nav: LeetCode
---

**二叉树(binary tree)**是一种基础数据结构。在二叉树中，每个节点除了自身保存的数据外还包含两个指针`left`和`right`分别指向左右两个子节点。因此python中二叉树(节点)的定义可参考如下：

```python
class TreeNode: 
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None
```
{: .snippet}

## 遍历

二叉树的经典问题是对树中的节点进行遍历。根据惯例，我们在访问子节点时会按照先左后右的顺序进行遍历。因此根据对当前节点的访问顺序二叉树的遍历可以分为**前序遍历(中左右)**、**中序遍历(左中右)**和**后序遍历(左右中)**三种。

### 144. 二叉树的前序遍历

给你二叉树的根节点`root`，返回它节点值的**前序**遍历。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg">
</div>

```
输入：root = [1,null,2,3]
输出：[1,2,3]
```

**示例2：**

```
输入：root = []
输出：[]
```

**示例3：**

```
输入：root = [1]
输出：[1]
```

**示例4：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/https://assets.leetcode.com/uploads/2020/09/15/inorder_5.jpg">
</div>

```
输入：root = [1,2]
输出：[1,2]
```

**示例5：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/09/15/inorder_4.jpg">
</div>

```
输入：root = [1,null,2]
输出：[1,2]
```

**提示：**

- 树中节点数目在范围`[0, 100]`内。
- -100 <= `Node.val` <= 100。

#### Solution

二叉树的遍历有着天然的递归结构，我们只需要按照访问顺序进行递归调用即可。

[题目链接](https://leetcode.cn/problems/binary-tree-preorder-traversal/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []
        
        return [root.val] + self.preorderTraversal(root.left) + self.preorderTraversal(root.right)
```
{: .snippet}

除了递归解法之外，我们还可以使用迭代来进行遍历。和递归相比，通过迭代进行的遍历可以减少函数调用的开销，因此在程序运行时有着更好的性能。二叉树遍历的迭代解法思路是利用栈来模拟程序的递归调用，其模板如下：

```
while stack or cur:
    while cur:
        stack.append(cur)
        cur 向下遍历
    
    node = stack.pop()
    使用 node 来更新 cur
```

前序遍历的特点是从当前节点沿左节点自上而下访问沿途节点，然后再自下而上访问沿途节点的右子树。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/VAD6jmh.png" width="80%">
</div>

因此利用循环模板可以得到如下代码。

[题目链接](https://leetcode.cn/problems/binary-tree-preorder-traversal/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []
        
        res = []
        stack = []
        cur = root

        while stack or cur:
            while cur:
                res.append(cur.val)

                stack.append(cur)
                cur = cur.left

            node = stack.pop()
            cur = node.right 
        
        return res
```
{: .snippet}

### 94. 二叉树的中序遍历

给定一个二叉树的根节点`root`，返回它的**中序**遍历。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg">
</div>

```
输入：root = [1,null,2,3]
输出：[1,3,2]
```

**示例2：**

```
输入：root = []
输出：[]
```

**示例3：**

```
输入：root = [1]
输出：[1]
```

**提示：**

- 树中节点数目在范围`[0, 100]`内。
- -100 <= `Node.val` <= 100。

#### Solution

中序遍历的递归解法与[前序遍历](/leetcode/2023-02-03-BinaryTree.html#144-二叉树的前序遍历)类似，只需调整节点上的相对访问顺序即可。

[题目链接](https://leetcode.cn/problems/binary-tree-inorder-traversal/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []
        
        return self.inorderTraversal(root.left) + [root.val] + self.inorderTraversal(root.right)
```
{: .snippet}

中序遍历的节点访问顺序是沿左节点，自下而上访问沿途节点及其右子树。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/9u57wmH.png" width="80%">
</div>

因此在迭代解法中只需要调整向`res`添加节点值的顺序即可，此时我们只在出栈时才将节点值添加到`res`中。

[题目链接](https://leetcode.cn/problems/binary-tree-inorder-traversal/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []
        
        res = []
        stack = []
        cur = root

        while stack or cur:
            while cur:
                stack.append(cur)
                cur = cur.left
            
            node = stack.pop()
            res.append(node.val)
            cur = node.right

        return res
```
{: .snippet}

### 145. 二叉树的后序遍历

给你一棵二叉树的根节点`root`，返回其节点值的**后序**遍历。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/https://assets.leetcode.com/uploads/2020/08/28/pre1.jpg">
</div>

```
输入：root = [1,null,2,3]
输出：[3,2,1]
```

**示例2：**

```
输入：root = []
输出：[]
```

**示例3：**

```
输入：root = [1]
输出：[1]
```

**提示：**

- 树中节点数目在范围`[0, 100]`内。
- -100 <= `Node.val` <= 100。

#### Solution

后序遍历的递归解法同样非常简单。

[题目链接](https://leetcode.cn/problems/binary-tree-postorder-traversal/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []
        
        return self.postorderTraversal(root.left) + self.postorderTraversal(root.right) + [root.val]
```
{: .snippet}

后序遍历的迭代解法与前序遍历基本一致，只不过需要先不断向下访问右节点然后再自下而上访问左子树。同时需要注意的是最后要把结果反序输出。

[题目链接](https://leetcode.cn/problems/binary-tree-postorder-traversal/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def postorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []
        
        res = []
        stack = []
        cur = root

        while stack or cur:
            while cur:
                res.append(cur.val)
                
                stack.append(cur)
                cur = cur.right
            
            node = stack.pop()
            cur = node.left

        return res[::-1]
```
{: .snippet}

### 102. 二叉树的层序遍历

给你二叉树的根节点`root`，返回其节点值的**层序遍历**。(即逐层地，从左到右访问所有节点)。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/02/19/tree1.jpg">
</div>

```
输入：root = [3,9,20,null,null,15,7]
输出：[[3],[9,20],[15,7]]
```

**示例2：**

```
输入：root = [1]
输出：[[1]]
```

**示例3：**

```
输入：root = []
输出：[]
```

**提示：**

- 树中节点数目在范围`[0, 2000]`内。
- -1000 <= `Node.val` <= 1000。

#### Solution

二叉树的另一种遍历方式是层序遍历。顾名思义，层序遍历会按照节点所在的层级从左到右依次进行遍历，它的本质是**广度优先搜索(breadth-first search, BFS)**。因此我们可以使用一个队列来存储位于同一层级的节点，然后依次进行访问。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/camo.githubusercontent.com/919d39fe06ad2477c184566959d71de2394c53628d4d7a2cc858087a3a1d113b/68747470733a2f2f636f64652d7468696e6b696e672e63646e2e626365626f732e636f6d2f676966732f3130322545342542412538432545352538462538392545362541302539312545372539412538342545352542312538322545352542412538462545392538312538442545352538452538362e676966" width="60%">
</div>

[题目链接](https://leetcode.cn/problems/binary-tree-level-order-traversal/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []

        from collections import deque

        res = []
        queue = deque([root])

        while queue:
            N = len(queue)
            level = []

            for i in range(N):
                node = queue.popleft()
                level.append(node.val)

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            res.append(level)

        return res
```
{: .snippet}

## 属性

### 101. 对称二叉树

给你一个二叉树的根节点`root`，检查它是否轴对称。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/02/19/symtree1.jpg">
</div>

```
输入：root = [1,2,2,3,4,4,3]
输出：true
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/02/19/symtree2.jpg">
</div>

```
输入：root = [1,2,2,null,3,null,3]
输出：false
```

**提示：**

- 树中节点数目在范围`[0, 1000]`内。
- -100 <= `Node.val` <= 100。

#### Solution

判断一棵树是否对称时我们需要考虑它的`left`和`right`两棵子树是否对称：

- 如果`left`和`right`均为空则**对称**；
- 如果`left`和`right`中一个为空另一个非空则**非对称**；
- 如果`left`和`right`均非空但`val`不相等则**非对称**；
- 如果`left`和`right`均非空且`val`相等则需要继续判断。

因此判断树是否对称具有天然的递归结构：当`left`和`right`非空且`val`相等时则需要进一步考虑树的内外两侧是否分别对称，只有当两侧都是对称时`left`和`right`才是对称的。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/camo.githubusercontent.com/c6b7e44d2d4a15a2ab7bf066addab1380aab6e9ce15491a4aaca04388abebc7b/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303231303230333134343632343431342e706e67" width="60%">
</div>

[题目链接](https://leetcode.cn/problems/symmetric-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        if not root:
            return True

        def compare(T1: Optional[TreeNode], T2: Optional[TreeNode]) -> bool:
            if not T1 and not T2:
                return True
            elif T1 and not T2:
                return False
            elif not T1 and T2:
                return False
            elif T1.val != T2.val:
                return False
            
            return compare(T1.left, T2.right) and compare(T1.right, T2.left)
        
        return compare(root.left, root.right)
```
{: .snippet}

我们同样可以使用迭代来处理这样的问题，整个比较过程可以如下：

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/camo.githubusercontent.com/6a9723fd0f9426d8d01fc02a286bf4d8e5fdbdf20360a17068c25e330cf562fd/68747470733a2f2f636f64652d7468696e6b696e672e63646e2e626365626f732e636f6d2f676966732f3130312e2545352541462542392545372541372542302545342542412538432545352538462538392545362541302539312e676966">
</div>

[题目链接](https://leetcode.cn/problems/symmetric-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        if not root:
            return True
        
        from collections import deque

        queue = deque([root.left, root.right])

        while queue:
            node1 = queue.popleft()
            node2 = queue.popleft()

            if not node1 and not node2:
                continue
            elif node1 and not node2:
                return False
            elif not node1 and node2:
                return False
            elif node1.val != node2.val:
                return False
            
            queue.append(node1.left)
            queue.append(node2.right)

            queue.append(node1.right)
            queue.append(node2.left)

        return True
```
{: .snippet}

除此之外也可以使用层次遍历来进行处理，此时只需要考虑每一层是否对称即可。

[题目链接](https://leetcode.cn/problems/symmetric-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        if not root:
            return True
        
        from collections import deque

        queue = deque([root.left, root.right])

        while queue:
            N = len(queue)
            for i in range(N//2):
                node1 = queue[i]
                node2 = queue[N-1-i]
                
                if not node1 and not node2:
                    continue
                elif node1 and not node2:
                    return False
                elif not node1 and node2:
                    return False
                elif node1.val != node2.val:
                    return False

            for i in range(N):
                node = queue.popleft()
                
                if node:
                    queue.append(node.left)
                    queue.append(node.right)
        
        return True
```
{: .snippet}

### 100. 相同的树

给你两棵二叉树的根节点`p`和`q`，编写一个函数来检验这两棵树是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/12/20/ex1.jpg">
</div>

```
输入：p = [1,2,3], q = [1,2,3]
输出：true
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/12/20/ex2.jpg">
</div>

```
输入：p = [1,2], q = [1,null,2]
输出：false
```

**示例3：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/12/20/ex3.jpg">
</div>

```
输入：p = [1,2,1], q = [1,1,2]
输出：false
```

**提示：**

- 两棵树上的节点数目都在范围`[0, 100]`内。
- -10⁴ <= `Node.val` <= 10⁴。

#### Solution

本题解法与[对称二叉树](/leetcode/2023-02-03-BinaryTree.html#101-对称二叉树)基本一致，只需分别判断两棵树的相应节点即可。

[题目链接](https://leetcode.cn/problems/same-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        if not p and not q:
            return True
        elif p and not q:
            return False
        elif not p and q:
            return False
        elif p.val != q.val:
            return False
        
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
```
{: .snippet}

### 572. 另一棵树的子树

给你两棵二叉树`root`和`subRoot`。检验`root`中是否包含和`subRoot`具有相同结构和节点值的子树。如果存在，返回`true`；否则，返回`false`。

二叉树`tree`的一棵子树包括`tree`的某个节点和这个节点的所有后代节点。`tree`也可以看做它自身的一棵子树。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/04/28/subtree1-tree.jpg">
</div>

```
输入：root = [3,4,5,1,2], subRoot = [4,1,2]
输出：true
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/04/28/subtree2-tree.jpg">
</div>

```
输入：root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
输出：false
```

**提示：**

- `root`树上的节点数量范围是`[1, 2000]`。
- `subRoot`树上的节点数量范围是`[1, 1000]`。
- -10⁴ <= `root.val` <= 10⁴。
- -10⁴ <= `subRoot.val` <= 10⁴。

#### Solution

本题解法可参考[相同的树](/leetcode/2023-02-03-BinaryTree.html#100-相同的树)。我们首先定义一个比较函数`compare(T1, T2)`用来判断两棵树是否相同，然后分别测试`root`与`subRoot`是否相同、`root.left`或者`root.right`是否包含`subRoot`即可。

[题目链接](https://leetcode.cn/problems/subtree-of-another-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        def compare(T1: Optional[TreeNode], T2: Optional[TreeNode]) -> bool:
            if not T1 and not T2:
                return True
            elif T1 and not T2:
                return False
            elif not T1 and T2:
                return False
            elif T1.val != T2.val:
                return False

            return compare(T1.left, T2.left) and compare(T1.right, T2.right)
        
        if not root and not subRoot:
            return True
        elif not root and subRoot:
            return False
        
        return compare(root, subRoot) or self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)
```
{: .snippet}

本题的迭代解法则需要使用广度优先或者深度优先对`root`进行遍历：如果找到相同的树则返回`True`，否则继续向下直到`root`中所有节点都进行过比较并最终返回`False`。

[题目链接](https://leetcode.cn/problems/subtree-of-another-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSubtree(self, root: Optional[TreeNode], subRoot: Optional[TreeNode]) -> bool:
        def compare(T1: Optional[TreeNode], T2: Optional[TreeNode]) -> bool:
            if not T1 and not T2:
                return True
            elif T1 and not T2:
                return False
            elif not T1 and T2:
                return False
            elif T1.val != T2.val:
                return False

            return compare(T1.left, T2.left) and compare(T1.right, T2.right)
        
        from collections import deque

        queue = deque([root])

        while queue:
            node = queue.popleft()
            if compare(node, subRoot):
                return True
            elif node:
                queue.append(node.left)
                queue.append(node.right)
        
        return False
```
{: .snippet}

### 104. 二叉树的最大深度

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

**说明: **叶子节点是指没有子节点的节点。

**示例：**
给定二叉树`[3,9,20,null,null,15,7]`，

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度`3`。

#### Solution

二叉树最大深度的基本解法是使用递归：我们先分别计算左子树和右子树的最大深度`d1`和`d2`，然后当前节点的最大深度等于`max(d1, d2)+1`。

[题目链接](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        d1 = self.maxDepth(root.left)
        d2 = self.maxDepth(root.right)

        return max(d1, d2)+1
```
{: .snippet}

而最大深度的迭代解法则类似于[层序遍历](/leetcode/2023-02-03-BinaryTree.html#102-二叉树的层序遍历)。我们使用一个变量`depth`来记录当前的深度，每深入一层就令`depth`加一。当队列为空时`depth`即为最大深度。

[题目链接](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        from collections import deque

        queue = deque([root])
        depth = 0

        while queue:
            N = len(queue)
            depth += 1

            for i in range(N):
                node = queue.popleft()

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        
        return depth
```
{: .snippet}

### 559. N叉树的最大深度

给定一个N叉树，找到其最大深度。

最大深度是指从根节点到最远叶子节点的最长路径上的节点总数。

N叉树输入按层序遍历序列化表示，每组子节点由空值分隔（请参见示例）。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2018/10/12/narytreeexample.png" width="50%">
</div>

```
输入：root = [1,null,3,2,4,null,5,6]
输出：3
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2019/11/08/sample_4_964.png" width="55%">
</div>

```
输入：root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
输出：5
```
#### Solution

本题解法与[二叉树最大深度](/leetcode/2023-02-03-BinaryTree.html#104-二叉树的最大深度)基本一致。

[题目链接](https://leetcode.cn/problems/maximum-depth-of-n-ary-tree/)：

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""

class Solution:
    def maxDepth(self, root: 'Node') -> int:
        if not root:
            return 0
        elif len(root.children) == 0:
            return 1
        
        return 1 + max([self.maxDepth(child) for child in root.children])
```
{: .snippet}

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""

class Solution:
    def maxDepth(self, root: 'Node') -> int:
        if not root:
            return 0
        
        from collections import deque

        queue = deque([root])
        depth = 0

        while queue:
            N = len(queue)
            depth += 1

            for i in range(N):
                node = queue.popleft()
                
                for child in node.children:
                    queue.append(child)
        
        return depth
```
{: .snippet}

### 111. 二叉树的最小深度

给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

**说明：**叶子节点是指没有子节点的节点。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/10/12/ex_depth.jpg">
</div>

```
输入：root = [3,9,20,null,null,15,7]
输出：2
```

**示例2：**

```
输入：root = [2,null,3,null,4,null,5,null,6]
输出：5
```

**提示：**

- 树中节点数的范围在`[0, 10⁵]`内。
- -1000 <= `Node.val` <= 1000。

#### Solution

本题解法与[二叉树最大深度](/leetcode/2023-02-03-BinaryTree.html#104-二叉树的最大深度)类似，但需要注意的是节点的最小深度并不是左右子树深度的最小值加1，而是需要考虑两棵子树是否存在：

- 如果左右两棵子树都存在，则当前节点的最小深度是两棵子树深度的最小值加1。
- 如果只有一棵子树存在，则当前节点的最小深度是存在子树的深度加1。
- 如果两棵子树都不存在，则当前节点的深度为1。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/6G1rJ9c.png" width="60%">
</div>

[题目链接](https://leetcode.cn/problems/minimum-depth-of-binary-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def minDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        if root.left and root.right:
            d1 = self.minDepth(root.left)
            d2 = self.minDepth(root.right)

            return 1 + min(d1, d2)
        elif root.left:
            return 1 + self.minDepth(root.left)
        elif root.right:
            return 1 + self.minDepth(root.right)
        else:
            return 1
```
{: .snippet}

基于层序遍历的迭代解法思路更加清晰：我们只需要在遍历节点时额外检查当前节点是否为叶节点，如果是叶节点就直接返回深度。

[题目链接](https://leetcode.cn/problems/minimum-depth-of-binary-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def minDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        from collections import deque

        queue = deque([root])
        depth = 0

        while queue:
            N = len(queue)
            depth += 1

            for i in range(N):
                node = queue.popleft()

                if not node.left and not node.right:
                    return depth
                
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

        return depth
```
{: .snippet}

### 222. 完全二叉树的节点个数

给你一棵**完全二叉树**的根节点`root`，求出该树的节点个数。

**完全二叉树**的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第`h`层，则该层包含`1~ 2ʰ`个节点。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/01/14/complete.jpg">
</div>

```
输入：root = [1,2,3,4,5,6]
输出：6
```

**示例2：**

```
输入：root = []
输出：0
```

**示例3：**

```
输入：root = [1]
输出：1
```

**提示：**

- 树中节点的数目范围是`[0, 5 * 10⁴]`。
- 0 <= `Node.val` <= 5*10⁴。
- 题目数据保证输入的树是**完全二叉树**。

#### Solution

首先按照一般的二叉树来进行求解，我们可以通过深度优先或是广度优先来对树进行遍历。深度优先的时间复杂度为`O(n)`，而空间复杂度为`O(log n)`。

[题目链接](https://leetcode.cn/problems/count-complete-tree-nodes/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def countNodes(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        cnt = 1

        if root.left:
            cnt += self.countNodes(root.left)
        if root.right:
            cnt += self.countNodes(root.right)

        return cnt
```
{: .snippet}

广度优先的时间复杂度为`O(n)`，而空间复杂度为`O(n)`。

[题目链接](https://leetcode.cn/problems/count-complete-tree-nodes/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def countNodes(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        from collections import deque

        queue = deque([root])
        cnt = 0

        while queue:
            N = len(queue)
            cnt += N

            for i in range(N):
                node = queue.popleft()

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        
        return cnt
```
{: .snippet}

本题的最优解法需要使用到**完全二叉树**的性质。根据定义，完全二叉树要么每一层都被填满，要么只有最下层没被填满。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/camo.githubusercontent.com/5d85c9f8df419ce8db22f668ff22f7a3ae55660b8e9bead3b98e2d8cdd69ac9c/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303230313132343039323534333636322e706e67" width="70%">
</div>

当二叉树每一层都填满时称为**满二叉树**，此时树中节点数量为`2ʰ-1`。在这种情况下我们只需要遍历树的深度就能够得到节点的总数量。而如果完全二叉树不是满二叉树，则只能分别统计两棵子树中节点的数量，然后树中节点总数等于两棵子树节点数量之和加1。这样可以得到递归代码如下，其时间复杂度为`O(log n × log n)`，而空间复杂度为`O(log n)`。

[题目链接](https://leetcode.cn/problems/count-complete-tree-nodes/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def countNodes(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        left = root.left
        right= root.right

        leftDepth = 0
        rightDepth= 0

        while left:
            leftDepth += 1
            left = left.left
        
        while right:
            rightDepth += 1
            right = right.right
        
        if leftDepth == rightDepth:
            return (2 << leftDepth) - 1
        
        return self.countNodes(root.left) + self.countNodes(root.right) + 1
```
{: .snippet}

### 110. 平衡二叉树

给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

- 一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过`1`。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/10/06/balance_1.jpg">
</div>

```
输入：root = [3,9,20,null,null,15,7]
输出：true
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/10/06/balance_2.jpg">
</div>

```
输入：root = [1,2,2,3,3,null,null,4,4]
输出：false
```

**示例3：**

```
输入：root = []
输出：true
```

**提示：**

- 树中的节点数在范围`[0, 5000]`内。
- -10⁴ <= `Node.val` <= 10⁴。

#### Solution

本题需要递归计算左右两棵子树的高度，因此我们需要定义一个辅助函数`getHeight(node)`：

- 首先计算左右两棵子树的高度，分别记录到`leftHeight`和`rightHeight`中；
- 当左子树或右子树不是高度平衡二叉树时返回`-1`，表示当前树不可能是高度平衡二叉树；
- 继续比较左右两棵子树的高度之差，如果大于`1`则返回`-1`表示表示当前树不是高度平衡二叉树；
- 最后返回当前树的高度`1 + max(leftHeight, rightHeight)`。

这样判断`root`是不是高度平衡二叉树只需要看`getHeight(root)`是否等于`-1`即可。

[题目链接](https://leetcode.cn/problems/balanced-binary-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        def getHeight(node: Optional[TreeNode]) -> int:
            if not node:
                return 0
            
            if (leftHeight := getHeight(node.left)) == -1:
                return -1
            if (rightHeight := getHeight(node.right)) == -1:
                return -1
            if abs(leftHeight - rightHeight) > 1:
                return -1
            return 1 + max(leftHeight, rightHeight)
        
        return getHeight(root) != -1
```
{: .snippet}

### 257. 二叉树的所有路径

给你一个二叉树的根节点`root`，按**任意顺序**，返回所有从根节点到叶子节点的路径。

**叶子节点**是指没有子节点的节点。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/03/12/paths-tree.jpg">
</div>

```
输入：root = [1,2,3,null,5]
输出：["1->2->5","1->3"]
```

**示例2：**

```
输入：root = [1]
输出：["1"]
```

**提示：**

- 树中的节点数在范围`[0, 100]`内。
- -100 <= `Node.val` <= 100。

#### Solution

本题的基本解法是深度优先搜索：我们自上而下对`root`进行遍历，每当遇到叶节点就构造一条路径添加到结果中。因此我们构造一个辅助函数`traverse()`，它需要3个输入参数：

- `node`表示当前节点；
- `path`记录了从`root`到`node`节点的路径；
- `res`用来保存所有的路径结果。

不难发现，整个遍历过程类似于[前序遍历](/leetcode/2023-02-03-BinaryTree.html#144-二叉树的前序遍历)。

[题目链接](https://leetcode.cn/problems/binary-tree-paths/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
        def traverse(node: Optional[TreeNode], path: str, res: List[str]) -> List[str]:

            if not node.left and not node.right:
                res.append(path)
                return res
            
            if node.left:
                res = traverse(node.left, path+"->"+str(node.left.val), res)
            if node.right:
                res = traverse(node.right, path+"->"+str(node.right.val), res)
            
            return res
        
        return traverse(root, str(root.val), [])
```
{: .snippet}

本题的另一种理解方式是**回溯**：当我们访问完叶节点后需要通过回溯的方式来回到上一层的父节点，然后再进入下一个路径。这样的过程可以使用栈来实现。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/pic.leetcode-cn.com/1662887575-zcfIKH-image.png"  width="70%">
</div>

[题目链接](https://leetcode.cn/problems/binary-tree-paths/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def binaryTreePaths(self, root: Optional[TreeNode]) -> List[str]:
        stack = [root]
        path_st = [str(root.val)]
        res = []

        while stack:
            node = stack.pop()
            path = path_st.pop()

            if (not node.left) and (not node.right):
                res.append(path)

                continue
            
            if node.right:
                stack.append(node.right)
                path_st.append(path + "->" + str(node.right.val))
            
            if node.left:
                stack.append(node.left)
                path_st.append(path + "->" + str(node.left.val))

        return res
```
{: .snippet}

### 404. 左叶子之和

给定二叉树的根节点`root`，返回所有左叶子之和。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/04/08/leftsum-tree.jpg">
</div>

```
输入: root = [3,9,20,null,null,15,7] 
输出: 24 
解释: 在这个二叉树中，有两个左叶子，分别是 9 和 15，所以返回 24
```

**示例2：**

```
输入: root = [1]
输出: 0
```

**提示：**

- 树中的节点数在范围`[0, 1000]`内。
- -1000 <= `Node.val` <= 1000。

#### Solution

本题的难点在于**左叶子**的定义，这里需要先明确它：

- 一个节点为**左叶子**节点，当且仅当它是某个节点的左子节点，并且它是一个叶子结点。

因此我们无法直接判断当前节点是否是一个左叶子节点，而必须借助它的父节点才能判断。明确定义后我们可以得到递归结构：

- 计算`root`左子树和右子树的左叶子之和，把它们加起来记录到`total`中；
- 如果`root.left`是左叶子节点，`total`还要再加上`root.left.val`；
- 返回`total`作为当前树的左叶子之和。

不难发现上面的结构类似于[后序遍历](/leetcode/2023-02-03-BinaryTree.html#145-二叉树的后序遍历)。

[题目链接](https://leetcode.cn/problems/sum-of-left-leaves/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        
        leftSum = self.sumOfLeftLeaves(root.left)
        rightSum= self.sumOfLeftLeaves(root.right)

        total = leftSum + rightSum
        if isLeaf(root.left):
            total += root.left.val

        return total

def isLeaf(root: Optional[TreeNode]) -> bool:
    if not root:
        return False
    
    return (not root.left) and (not root.right)
```
{: .snippet}

本题同样可以使用迭代来进行处理。此时只需要不断检查当前节点的左节点是否是左叶子节点即可，代码可参考如下：

[题目链接](https://leetcode.cn/problems/sum-of-left-leaves/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
        stack = [root]
        res = 0

        while stack:
            node = stack.pop()

            if isLeaf(node.left):
                res += node.left.val
            
            if node.left:
                stack.append(node.left)
            if node.right:
                stack.append(node.right)
        
        return res

def isLeaf(root: Optional[TreeNode]) -> bool:
    if not root:
        return False
    
    return (not root.left) and (not root.right)
```
{: .snippet}

### 513. 找树左下角的值

给定一个二叉树的 **根节点** `root`，请找出该二叉树的 **最底层** **最左边** 节点的值。

假设二叉树中至少有一个节点。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/12/14/tree1.jpg">
</div>

```
输入: root = [2,1,3]
输出: 1
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/12/14/tree2.jpg">
</div>

```
输入: [1,2,3,4,null,5,6,null,null,7]
输出: 7
```

**提示：**

- 树中的节点数在范围`[1, 10⁴]`内。
- -2³² <= `Node.val` <= 2³²-1。

#### Solution

本题的基本解法是使用[层序遍历](/leetcode/2023-02-03-BinaryTree.html#102-二叉树的层序遍历)。根据题意，我们只需要用每一层最左边节点的值来更新`res`即可。完成遍历后`res`的值即为二叉树最底层最左边节点的值。

[题目链接](https://leetcode.cn/problems/find-bottom-left-tree-value/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def findBottomLeftValue(self, root: Optional[TreeNode]) -> int:
        from collections import deque

        queue = deque([root])
        res = 0

        while queue:
            N = len(queue)
            res = queue[0].val

            for i in range(N):
                node = queue.popleft()

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        
        return res
```
{: .snippet}

本题的另一种解法是使用深度优先搜索。我们需要分别遍历左节点和右节点，然后返回两棵子树最底层最左边节点的值以及对应的深度。这样当前树最底层最左边的值即为两棵子树中拥有最大深度树的返回节点值，相应代码可以参考如下。

[题目链接](https://leetcode.cn/problems/find-bottom-left-tree-value/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def findBottomLeftValue(self, root: Optional[TreeNode]) -> int:
        def traversal(node: Optional[TreeNode], depth: int):
            if not node:
                return 0, 0
            elif (not node.left) and (not node.right):
                return node.val, depth
            
            leftVal, leftDepth = traversal(node.left, depth+1)
            rightVal, rightDepth = traversal(node.right, depth+1)

            if leftDepth >= rightDepth:
                return leftVal, leftDepth
            else:
                return rightVal, rightDepth
        
        res, _ = traversal(root, 0)

        return res
```
{: .snippet}

### 112. 路径总和

给你二叉树的根节点`root`和一个表示目标和的整数`targetSum`。判断该树中是否存在**根节点到叶子节点**的路径，这条路径上所有节点值相加等于目标和`targetSum`。如果存在，返回`true`；否则，返回`false`。

**叶子节点**是指没有子节点的节点。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/01/18/pathsum1.jpg">
</div>

```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,null,1], targetSum = 22
输出：true
解释：等于目标和的根节点到叶节点路径如上图所示。
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg">
</div>

```
输入：root = [1,2,3], targetSum = 5
输出：false
解释：树中存在两条根节点到叶子节点的路径：
(1 --> 2): 和为 3
(1 --> 3): 和为 4
不存在 sum = 5 的根节点到叶子节点的路径。
```

**示例3：**

```
输入：root = [], targetSum = 0
输出：false
解释：由于树是空的，所以不存在根节点到叶子节点的路径。
```

**提示：**

- 树中的节点数在范围`[0, 5000]`内。
- -1000 <= `Node.val` <= 1000。
- -1000 <= `targetSum` <= 1000。

#### Solution

本题可以使用深度优先搜索来求解。我们只需要分别递归遍历左子树和右子树，只要其中存在满足要求的路径即可。

[题目链接](https://leetcode.cn/problems/path-sum/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if not root:
            return False
        
        if (not root.left) and (not root.right):
            return root.val == targetSum
        else:
            return self.hasPathSum(root.left, targetSum-root.val) or self.hasPathSum(root.right, targetSum-root.val)
```
{: .snippet}

本题的另一种求解思路是使用回溯。这里我们需要两个栈来分别存储当前遍历到的节点以及路径上节点值之和，这样就可以利用出栈来模拟回溯的过程。具体代码可参考如下。

[题目链接](https://leetcode.cn/problems/path-sum/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if not root:
            return False
        
        stack = [root]
        val_st= [root.val]

        while stack:
            node = stack.pop()
            val  = val_st.pop()

            if (not node.left) and (not node.right) and val == targetSum:
                return True
            
            if node.right:
                stack.append(node.right)
                val_st.append(val+node.right.val)
            if node.left:
                stack.append(node.left)
                val_st.append(val+node.left.val)

        return False
```
{: .snippet}

### 113. 路径总和II

给你二叉树的根节点`root`和一个整数目标和`targetSum`，找出所有**从根节点到叶子节点**路径总和等于给定目标和的路径。

**叶子节点**是指没有子节点的节点。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/01/18/pathsumii1.jpg">
</div>

```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg">
</div>

```
输入：root = [1,2,3], targetSum = 5
输出：[]
```

**示例3：**

```
输入：root = [1,2], targetSum = 0
输出：[]
```

**提示：**

- 树中的节点数在范围`[0, 5000]`内。
- -1000 <= `Node.val` <= 1000。
- -1000 <= `targetSum` <= 1000。

#### Solution

本题解法与[路径总和](/leetcode/2023-02-03-BinaryTree.html#112-路径总和)基本一致，不过需要注意的是在进行递归时要保存中间结果。

[题目链接](https://leetcode.cn/problems/path-sum-ii/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        def traversal(root, target, path, res) -> List[List[int]]:
            if not root:
                return res
            
            if (not root.left) and (not root.right):
                if root.val == target:
                    res.append(path)
                return res
            
            if root.left:
                res = traversal(root.left, target-root.val, path+[root.left.val], res)
            if root.right:
                res = traversal(root.right, target-root.val, path+[root.right.val], res)
            
            return res
        
        if not root:
            return []
        
        return traversal(root, targetSum, [root.val], [])
```
{: .snippet}

本题的回溯解法相对比较简单，代码可参考如下。

[题目链接](https://leetcode.cn/problems/path-sum-ii/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        if not root:
            return []
        
        stack   = [root]
        val_st  = [root.val]
        path_st = [[root.val]]
        res = []

        while stack:
            node = stack.pop()
            val  = val_st.pop()
            path = path_st.pop()

            if (not node.left) and (not node.right) and val == targetSum:
                res.append(path)
            
            if node.right:
                stack.append(node.right)
                val_st.append(val + node.right.val)
                path_st.append(path + [node.right.val])
            
            if node.left:
                stack.append(node.left)
                val_st.append(val + node.left.val)
                path_st.append(path + [node.left.val])
        
        return res
```
{: .snippet}

## 修改与构造

### 226. 翻转二叉树

给你一棵二叉树的根节点`root`，翻转这棵二叉树，并返回其根节点。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/03/14/invert1-tree.jpg">
</div>

```
输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/03/14/invert2-tree.jpg">
</div>

```
输入：root = [2,1,3]
输出：[2,3,1]
```

**示例3：**

```
输入：root = []
输出：[]
```

**提示：**

- 树中节点数目在范围`[0, 100]`内。
- -100 <= `Node.val` <= 100。

#### Solution

翻转二叉树是二叉树的经典问题，利用问题自身的递归结构我们可以很容易地得到递归版本的代码。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/camo.githubusercontent.com/13127773de2a6e9e2cb7de066f108c74901df17a16abda07042f639d920317ff/68747470733a2f2f636f64652d7468696e6b696e672e63646e2e626365626f732e636f6d2f676966732f2545372542462542422545382542442541432545342542412538432545352538462538392545362541302539312e676966" width="60%">
</div>

[题目链接](https://leetcode.cn/problems/invert-binary-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return root

        root.left, root.right = self.invertTree(root.right), self.invertTree(root.left)
        
        return root
```
{: .snippet}

当然我们也可以基于迭代来实现翻转，此时只需要利用栈或队列来保存中间节点即可。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root:
            return root

        stack = [root]

        while stack:
            node = stack.pop()
            node.left, node.right = node.right, node.left

            if node.left:
                stack.append(node.left)
            
            if node.right:
                stack.append(node.right)
        
        return root
```
{: .snippet}

### 106. 从中序与后序遍历序列构造二叉树

给定两个整数数组`inorder`和`postorder`，其中`inorder`是二叉树的中序遍历，`postorder`是同一棵树的后序遍历，请你构造并返回这棵**二叉树**。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/02/19/tree.jpg">
</div>

```
输入：inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
输出：[3,9,20,null,null,15,7]
```

**示例2：**

```
输入：inorder = [-1], postorder = [-1]
输出：[-1]
```

**提示：**

- 1 <= `inorder.length` <= 3000。
- `postorder.length` == `inorder.length`。
- -3000 <= `inorder[i]`, `postorder[i]` <= 3000。
- `inorder`和`postorder`都由**不同**的值组成。
- `postorder`中每一个值都在`inorder`中。
- `inorder`**保证**是树的中序遍历。
- `postorder`**保证**是树的后序遍历。

#### Solution

本题需要结合[中序遍历](/leetcode/2023-02-03-BinaryTree.html#94-二叉树的中序遍历)和[后序遍历](/leetcode/2023-02-03-BinaryTree.html#145-二叉树的后序遍历)的顺序进行求解。回忆中序遍历的顺序为**左-中-右**，而后序遍历为**左-右-中**，因此`postorder`的末尾一定是当前的`root`。接下来利用`root`把`inorder`拆成`inorderLeft`和`inorderRight`两部分，分别对应`root.left`和`root.right`的中序遍历。类似地，我们还需要再把`postorder`同样拆成`postorderLeft`和`postorderRight`对应后序遍历的左右子树。由于`inorderLeft`和`postorderLeft`一定具有相同的长度，我们可以直接对`postorder`进行拆分。加下来只需要分别递归构造`root.left`和`root.right`即可。整个算法过程可以参考下图。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/gG6Z7vv.png">
</div>

[题目链接](https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, inorder: List[int], postorder: List[int]) -> Optional[TreeNode]:
        if not postorder:
            return None
        
        ## the last one in postorder is the root
        val = postorder[-1]
        root= TreeNode(val)

        ## split idx
        idx = inorder.index(val)

        inorderLeft = inorder[:idx]
        inorderRight= inorder[idx+1:]

        postorderLeft = postorder[:len(inorderLeft)]
        postorderRight= postorder[len(inorderLeft):-1]

        ## recursively build root.left and root.right
        root.left = self.buildTree(inorderLeft, postorderLeft)
        root.right= self.buildTree(inorderRight, postorderRight)

        return root
```
{: .snippet}

### 105. 从前序与中序遍历序列构造二叉树

给定两个整数数组`preorder`和`inorder`，其中`preorder`是二叉树的**先序遍历**，`inorder`是同一棵树的**中序遍历**，请构造二叉树并返回其根节点。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/02/19/tree.jpg">
</div>

```
输入: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
输出: [3,9,20,null,null,15,7]
```

**示例2：**

```
输入: preorder = [-1], inorder = [-1]
输出: [-1]
```

**提示：**

- 1 <= `preorder.length` <= 3000。
- `inorder.length` == `preorder.length`。
- -3000 <= `preorder[i]`, `inorder[i]` <= 3000。
- `preorder`和`inorder`均**无重复**元素。
- `inorder`中每一个值都在`preorder`中。
- `preorder`**保证**为二叉树的前序遍历序列。
- `inorder`**保证**为二叉树的中序遍历序列。

#### Solution

本题解法与[从中序与后序遍历序列构造二叉树](/leetcode/2023-02-03-BinaryTree.html#106-从中序与后序遍历序列构造二叉树)基本一致，唯一需要注意的是`preorder`的第一个元素对应了`root`节点。需要额外说明的是如果给定前序和后序遍历是**无法**确定唯一的二叉树的，这是因为没有中序遍历无法确定`root`左右部分，也就是无法完成分割。

[题目链接](https://leetcode.cn/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        if not preorder:
            return None
        
        ## the first one in preorder is the root
        val = preorder[0]
        root= TreeNode(val)

        ## split idx
        idx = inorder.index(val)

        inorderLeft = inorder[:idx] 
        inorderRight= inorder[idx+1:]

        preorderLeft = preorder[1:len(inorderLeft)+1]
        preorderRight= preorder[1+len(inorderLeft):]

        ## recursively build root.left and root.right
        root.left = self.buildTree(preorderLeft, inorderLeft)
        root.right= self.buildTree(preorderRight, inorderRight)

        return root
```
{: .snippet}

### 654. 最大二叉树

给定一个不重复的整数数组`nums`。**最大二叉树**可以用下面的算法从`nums`递归地构建:

- 创建一个根节点，其值为`nums`中的最大值。
- 递归地在最大值**左边**的**子数组前缀上**构建左子树。
- 递归地在最大值**右边**的**子数组后缀上**构建右子树。

返回`nums`构建的**最大二叉树**。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/12/24/tree1.jpg">
</div>

```
输入：nums = [3,2,1,6,0,5]
输出：[6,3,5,null,2,0,null,null,1]
解释：递归调用如下所示：
- [3,2,1,6,0,5] 中的最大值是 6 ，左边部分是 [3,2,1] ，右边部分是 [0,5] 。
    - [3,2,1] 中的最大值是 3 ，左边部分是 [] ，右边部分是 [2,1] 。
        - 空数组，无子节点。
        - [2,1] 中的最大值是 2 ，左边部分是 [] ，右边部分是 [1] 。
            - 空数组，无子节点。
            - 只有一个元素，所以子节点是一个值为 1 的节点。
    - [0,5] 中的最大值是 5 ，左边部分是 [0] ，右边部分是 [] 。
        - 只有一个元素，所以子节点是一个值为 0 的节点。
        - 空数组，无子节点。
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/12/24/tree2.jpg">
</div>

```
输入：nums = [3,2,1]
输出：[3,null,2,null,1]
```

**提示：**

- 1 <= `nums.length` <= 1000。
- 0 <= `nums[i]` <= 1000。
- `nums`中的所有整数**互不相同**。

#### Solution

本题只需要按照题干给出的递归算法进行实现即可。

[题目链接](https://leetcode.cn/problems/maximum-binary-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def constructMaximumBinaryTree(self, nums: List[int]) -> Optional[TreeNode]:
        if not nums:
            return None
        
        val = nums[0]
        idx = 0

        for i, num in enumerate(nums):
            if num > val:
                val = num
                idx = i
        
        root = TreeNode(val)

        ## recursively build root.left and root.right
        root.left = self.constructMaximumBinaryTree(nums[:idx])
        root.right= self.constructMaximumBinaryTree(nums[idx+1:])

        return root
```
{: .snippet}

### 617. 合并二叉树

给你两棵二叉树：`root1`和`root2`。

想象一下，当你将其中一棵覆盖到另一棵之上时，两棵树上的一些节点将会重叠（而另一些不会）。你需要将这两棵树合并成一棵新二叉树。合并的规则是：如果两个节点重叠，那么将这两个节点的值相加作为合并后节点的新值；否则，不为`null`的节点将直接作为新二叉树的节点。

返回合并后的二叉树。

**注意**: 合并过程必须从两个树的根节点开始。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/02/05/merge.jpg">
</div>

```
输入：root1 = [1,3,2,5], root2 = [2,1,3,null,4,null,7]
输出：[3,4,5,5,4,null,7]
```

**示例2：**

```
输入：root1 = [1], root2 = [1,2]
输出：[2,2]
```

**提示：**

- 两棵树中的节点数目在范围`[0, 2000]`内。
- -10⁴ <= `Node.val` <= 10⁴。

#### Solution

本题的递归解法非常直观，我们只需要融合根节点`root1`和`root2`然后递归地融合左右节点即可。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/OrMVBCh.gif">
</div>

[题目链接](https://leetcode.cn/problems/merge-two-binary-trees/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root1:
            return root2
        elif not root2:
            return root1
        
        root = TreeNode(root1.val+root2.val)
        root.left = self.mergeTrees(root1.left, root2.left)
        root.right= self.mergeTrees(root1.right, root2.right)

        return root
```
{: .snippet}

本题的迭代解法要相对麻烦一些。我们的整体思路是基于[层序遍历](/leetcode/2023-02-03-BinaryTree.html#102-二叉树的层序遍历)，每次向队列中添加两棵树的对应节点并进行更新：

- 如果两个节点都有左节点，则将两个左节点添加到队列中；
- 如果两个节点都有右节点，则将两个右节点添加到队列中。

这样可以保证队列中的前两个节点都是有效的节点，也因此当前节点的`val`等于两个节点`val`之和。接下来考虑两个节点中只有一个节点有左节点或右节点的情况，此时只要把该节点的左节点或右节点直接连接到当前节点上即可。整个算法流程可以参考如下。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/4UTn2Mj.gif" width="80%">
</div>

[题目链接](https://leetcode.cn/problems/merge-two-binary-trees/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root1:
            return root2
        elif not root2:
            return root1

        from collections import deque
        
        queue = deque([root1, root2])

        while queue:
            node1 = queue.popleft()
            node2 = queue.popleft()

            if node1.left and node2.left:
                queue.append(node1.left)
                queue.append(node2.left)
            
            if node1.right and node2.right:
                queue.append(node1.right)
                queue.append(node2.right)
            
            node1.val += node2.val

            if not node1.left and node2.left: 
                node1.left = node2.left
            if not node1.right and node2.right: 
                node1.right = node2.right

        return root1
```
{: .snippet}

## 二叉搜索树

### 700. 二叉搜索树中的搜索

给定二叉搜索树(BST)的根节点`root`和一个整数值`val`。

你需要在BST中找到节点值等于`val`的节点。返回以该节点为根的子树。如果节点不存在，则返回`null`。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/01/12/tree1.jpg">
</div>

```
输入：root = [4,2,7,1,3], val = 2
输出：[2,1,3]
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/01/12/tree2.jpg">
</div>

```
输入：root = [4,2,7,1,3], val = 5
输出：[]
```

**提示：**

- 数中节点数在`[1, 5000]`范围内。
- 1 <= `Node.val` <= 10⁷。
- `root`是二叉搜索树。
- 1 <= `val` <= 10⁷。

#### Solution

二叉搜索树的递归遍历比较容易：

- 当`root.val == val`时返回`root`；
- 当`root.val < val`时向下对右节点继续遍历；
- 当`root.val > val`时向下对左节点继续遍历。

[题目链接](https://leetcode.cn/problems/search-in-a-binary-search-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def searchBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        if not root:
            return None
        elif root.val == val:
            return root
        elif root.val < val:
            return self.searchBST(root.right, val)
        else:
            return self.searchBST(root.left, val)
```
{: .snippet}

而二叉搜索树的迭代遍历也比二叉树的迭代要容易一些。此时我们不再需要借助栈来进行回溯，直接向下遍历即可。

[题目链接](https://leetcode.cn/problems/search-in-a-binary-search-tree/)：

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def searchBST(self, root: Optional[TreeNode], val: int) -> Optional[TreeNode]:
        node = root

        while node:
            if node.val == val:
                return node
            elif node.val < val:
                node = node.right
            else:
                node = node.left
        
        return None
```
{: .snippet}

## Reference

- [二叉树理论基础](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)
- [关于二叉树，你该了解这些！](https://www.bilibili.com/video/BV1Hy4y1t7ij/?vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：144.二叉树的前序遍历 145.二叉树的后序遍历 94.二叉树的中序遍历](https://www.bilibili.com/video/BV1Wh411S7xt/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [二叉树的非递归遍历](https://www.bilibili.com/video/BV15f4y1W7i2/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [二叉树的非递归遍历-中序](https://www.bilibili.com/video/BV1Zf4y1a77g/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：6.翻转二叉树](https://www.bilibili.com/video/BV1sP4y1f7q7/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
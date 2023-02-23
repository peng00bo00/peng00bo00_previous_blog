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

因此利用循环模板可以得到如下代码：

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
            layer = []

            for i in range(N):
                node = queue.popleft()
                layer.append(node.val)

                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            res.append(layer)

        return res
```
{: .snippet}

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

## 比较

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

## 深度

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
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2018/10/12/narytreeexample.png" width=50%>
</div>

```
输入：root = [1,null,3,2,4,null,5,6]
输出：3
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2019/11/08/sample_4_964.png" width=55%>
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
<img src="https://pic1.xuehuaimg.com/proxy/camo.githubusercontent.com/93b85ef3d6e7a070f3281f4cf8949ec7affb07261311f989848ce2e7167ef5b6/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303231303230333135353830303530332e706e67" width=60%>
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

## Reference

- [二叉树理论基础](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)
- [关于二叉树，你该了解这些！](https://www.bilibili.com/video/BV1Hy4y1t7ij/?vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：144.二叉树的前序遍历 145.二叉树的后序遍历 94.二叉树的中序遍历](https://www.bilibili.com/video/BV1Wh411S7xt/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [二叉树的非递归遍历](https://www.bilibili.com/video/BV15f4y1W7i2/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [二叉树的非递归遍历-中序](https://www.bilibili.com/video/BV1Zf4y1a77g/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：6.翻转二叉树](https://www.bilibili.com/video/BV1sP4y1f7q7/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
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
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg" width="22%">
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
<img src="https://pic1.xuehuaimg.com/proxy/https://assets.leetcode.com/uploads/2020/09/15/inorder_5.jpg" width="22%">
</div>

```
输入：root = [1,2]
输出：[1,2]
```

**示例5：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/09/15/inorder_4.jpg" width="22%">
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

除了递归解法之外，我们还可以使用循环来进行遍历。和递归相比，通过循环进行的遍历可以减少函数调用的开销，因此在程序运行时有着更好的性能。二叉树遍历的迭代解法思路是利用栈来模拟程序的递归调用，其模板如下：

```
while stack or cur:
    while cur:
        stack.append(cur)
        cur 向下遍历
    
    tmp = stack.pop()
    使用 tmp 来更新 cur
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
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg" width="22%">
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

因此在循环解法中只需要调整向`res`添加节点值的顺序即可，此时我们只在出栈时才将节点值添加到`res`中。

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
<img src="https://pic1.xuehuaimg.com/proxy/https://assets.leetcode.com/uploads/2020/08/28/pre1.jpg" width="22%">
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
        
        stack = [root]
        res = []

        while stack:
            node = stack.pop()
            res.append(node.val)

            if node.left:
                stack.append(node.left)

            if node.right:
                stack.append(node.right)
        
        return res[::-1]
```
{: .snippet}

### 102. 二叉树的层序遍历

给你二叉树的根节点`root`，返回其节点值的**层序遍历**。(即逐层地，从左到右访问所有节点)。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/02/19/tree1.jpg" width="25%">
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
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/03/14/invert1-tree.jpg" width="80%">
</div>

```
输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/assets.leetcode.com/uploads/2021/03/14/invert2-tree.jpg" width="70%">
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

## Reference

- [二叉树理论基础](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)
- [关于二叉树，你该了解这些！](https://www.bilibili.com/video/BV1Hy4y1t7ij/?vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：144.二叉树的前序遍历 145.二叉树的后序遍历 94.二叉树的中序遍历](https://www.bilibili.com/video/BV1Wh411S7xt/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [二叉树的非递归遍历](https://www.bilibili.com/video/BV15f4y1W7i2/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [二叉树的非递归遍历-中序](https://www.bilibili.com/video/BV1Zf4y1a77g/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：6.翻转二叉树](https://www.bilibili.com/video/BV1sP4y1f7q7/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
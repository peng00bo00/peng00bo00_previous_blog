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

```python
class TreeNode: 
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None
```
{: .snippet}

## 遍历

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

        stack = [root]
        res = []

        while stack:
            node = stack.pop()
            res.append(node.val)

            if node.right:
                stack.append(node.right)
            
            if node.left:
                stack.append(node.left)
        
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
        
        stack = []
        res = []
        node = root

        while node or stack:
            if node:
                stack.append(node)
                node = node.left
            else:
                node = stack.pop()
                res.append(node.val)
                node = node.right
        
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
---
layout: article
title: 链表
key: leetcode-02
clipboard: true
aside:
  toc: true
sidebar:
  nav: LeetCode
---

**链表(linked list)**是一种通过指针串联在一起的线性结构，其中的每一个元素称为一个**节点(node)**。以单向链表为例，它的每个节点包含一个数据域用来存放数据，同时每个节点还包含一个指针域指向它的下一个节点。

<div align=center>
<img src="https://i.imgur.com/RKgLwHR.png" width="80%">
</div>

## 删除节点

### 203. 移除链表元素

给你一个链表的头节点`head`和一个整数`val`，请你删除链表中所有满足`Node.val == val`的节点，并返回**新的头节点**。

**示例1：**

```
输入：head = [1,2,6,3,4,5,6], val = 6
输出：[1,2,3,4,5]
```

**示例2：**

```
输入：head = [], val = 1
输出：[]
```

**示例3：**

```
输入：head = [7,7,7,7], val = 7
输出：[]
```

**提示：**

- 列表中的节点数目在范围`[0, 10⁴]`内。
- 1 <= `Node.val` <= 50。
- 0 <= `val` <= 50。

#### Solution

删除元素是链表的基本操作之一。由于我们不能像数组那样直接通过索引来获取节点，在删除元素时需要通过循环的方式来对整个链表进行遍历。在进行循环时我们首先为链表添加一个虚拟头节点(哨兵节点)`sentinel`，然后从它出发依次检验它的下一个节点是否包含`val`，如果包含则另当前节点指向再下一个节点。最后返回`sentinel`的后继节点即可。

[题目链接](https://leetcode.cn/problems/remove-linked-list-elements/)：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        sentinel = ListNode(next=head)
        node = sentinel

        while node.next is not None:
            if node.next.val == val:
                node.next = node.next.next
            else:
                node = node.next
        
        return sentinel.next
```
{: .snippet}

除了循环之外，我们也可以使用递归来处理删除节点的问题。每次调用函数时我们只检查当前的节点是否包含`val`，如果包含则把后继节点作为函数输入。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        if head is None:
            return head
        
        if head.val != val:
            head.next = self.removeElements(head.next, val)
            return head
        else:
            return self.removeElements(head.next, val)
```
{: .snippet}

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

删除元素是链表的基本操作之一。由于我们不能像数组那样直接通过索引来获取节点，在删除元素时需要通过循环的方式来对整个链表进行遍历。在进行循环时我们首先为链表添加一个**虚拟头节点(哨兵节点)**`sentinel`，它指向链表的头节点`head`。然后从`sentinel`出发依次检验它的下一个节点是否包含`val`，如果包含则另当前节点指向再下一个节点。最后返回`sentinel`的后继节点即可。

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

### 19. 删除链表的倒数第N个结点

给你一个链表，删除链表的倒数第`n`个结点，并且返回链表的头结点。

**示例1：**

```
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```

**示例2：**

```
输入：head = [1], n = 1
输出：[]
```

**示例3：**

```
输入：head = [1,2], n = 1
输出：[1]
```

**提示：**

- 链表中结点的数目为`sz`。
- 1 <= `sz` <= 30。
- 0 <= `Node.val` <= 100。
- 1 <= `n` <= `sz`。

#### Solution

本题的暴力解法是先对链表进行遍历从而得到它的大小`sz`然后删除第`sz-n`个节点，这种做法需要对链表进行两次遍历。实际上利用双指针只要一次遍历就可以实现相同的效果：我们首先为链表设置一个哨兵节点`sentinel`并且令`fast`和`slow`两个指针都指向它；然后令快指针`fast`前进`n`步使得两个指针之间的间隔恰好为`n`；最后让两个指针同时前进，当`fast`指向链表末尾节点时`slow`会指向倒数`n`个节点的前一个节点，此时只要删除`slow`的下一个节点即可。

使用双指针的算法流程可以参考下图：

<div align=center>
<img src="https://i.imgur.com/UG0xBSu.png" width="80%">
</div>

[题目链接](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        sentinel = ListNode(next=head)
        fast, slow = sentinel, sentinel

        for _ in range(n):
            fast = fast.next
        
        while fast.next is not None:
            fast = fast.next
            slow = slow.next
        
        slow.next = slow.next.next
        
        return sentinel.next
```
{: .snippet}

## 设计链表

### 707. 设计链表

设计链表的实现。您可以选择使用单链表或双链表。单链表中的节点应该具有两个属性：`val`和`next`。`val`是当前节点的值，`next`是指向下一个节点的指针/引用。如果要使用双向链表，则还需要一个属性`prev`以指示链表中的上一个节点。假设链表中的所有节点都是 0-index 的。

在链表类中实现这些功能：

- get(index)：获取链表中第`index`个节点的值。如果索引无效，则返回`-1`。
- addAtHead(val)：在链表的第一个元素之前添加一个值为`val`的节点。插入后，新节点将成为链表的第一个节点。
- addAtTail(val)：将值为`val`的节点追加到链表的最后一个元素。
- addAtIndex(index,val)：在链表中的第`index`个节点之前添加值为`val` 的节点。如果`index`等于链表的长度，则该节点将附加到链表的末尾。如果`index`大于链表长度，则不会插入节点。如果`index`小于0，则在头部插入节点。
- deleteAtIndex(index)：如果索引`index`有效，则删除链表中的第`index`个节点。

**示例：**

```
MyLinkedList linkedList = new MyLinkedList();
linkedList.addAtHead(1);
linkedList.addAtTail(3);
linkedList.addAtIndex(1,2);   //链表变为1-> 2-> 3
linkedList.get(1);            //返回2
linkedList.deleteAtIndex(1);  //现在链表是1-> 3
linkedList.get(1);            //返回3
```

**提示：**

- 0 <= `index`, `val` <= 1000。
- 请不要使用内置的 LinkedList 库。
- `get`, `addAtHead`, `addAtTail`, `addAtIndex`和`deleteAtIndex`的操作次数不超过`2000`。

#### Solution

[题目链接](https://leetcode.cn/problems/design-linked-list/)：

```python
class Node(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class MyLinkedList:

    def __init__(self):
        self.head = Node(-1)
        self.size = 0

    def get(self, index: int) -> int:
        if index < 0 or index >= self.size:
            return -1
        
        dummy = self.head.next

        for _ in range(index):
            dummy = dummy.next

        return dummy.val

    def addAtHead(self, val: int) -> None:
        node = Node(val, self.head.next)
        self.head.next = node
        self.size += 1

    def addAtTail(self, val: int) -> None:
        dummy = self.head
        for _ in range(self.size):
            dummy = dummy.next
        
        dummy.next = Node(val)

        self.size += 1

    def addAtIndex(self, index: int, val: int) -> None:
        if index < 0:
            return self.addAtHead(val)
        elif index == self.size:
            return self.addAtTail(val)
        elif index > self.size:
            return
        
        dummy = self.head
        for _ in range(index):
            dummy = dummy.next
        
        node = Node(val, dummy.next)
        dummy.next = node

        self.size += 1

    def deleteAtIndex(self, index: int) -> None:
        if index < 0 or index >= self.size:
            return
        
        dummy = self.head
        for _ in range(index):
            dummy = dummy.next
        
        dummy.next = dummy.next.next

        self.size -= 1
```
{: .snippet}

## 翻转链表

### 206.反转链表

给你单链表的头节点`head`，请你反转链表，并返回反转后的链表。

**示例1：**

```
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
```

**示例2：**

```
输入：head = [1,2]
输出：[2,1]
```

**示例3：**

```
输入：head = []
输出：[]
```

**提示：**

- 链表中节点的数目范围是`[0, 5000]`。
- -5000 <= `Node.val` <= 5000。

#### Solution

[题目链接](https://leetcode.cn/problems/reverse-linked-list/)：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        pre, cur = None, head

        while cur is not None:
            tmp = cur
            cur = cur.next

            tmp.next = pre
            pre = tmp
        
        return pre
```
{: .snippet}

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None or head.next is None:
            return head
        
        newhead = self.reverseList(head.next)
        head.next.next = head
        head.next = None

        return newhead
```
{: .snippet}

## 两两交换链表中的节点

### 24. 两两交换链表中的节点

给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）。

**示例1：**

```
输入：head = [1,2,3,4]
输出：[2,1,4,3]
```

**示例2：**

```
输入：head = []
输出：[]
```

**示例3：**

```
输入：head = [1]
输出：[1]
```

**提示：**

- 链表中节点的数目在范围`[0, 100]`内。
- 0 <= `Node.val` <= 100。

#### Solution

[题目链接](https://leetcode.cn/problems/swap-nodes-in-pairs/)：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        sentinel = ListNode(next=head)
        cur = sentinel

        while cur.next and cur.next.next:
            first, second = cur.next, cur.next.next

            first.next = second.next
            second.next = first
            cur.next = second

            cur = cur.next.next

        return sentinel.next
```
{: .snippet}

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None or head.next is None:
            return head
        
        first, second = head, head.next

        first.next = self.swapPairs(second.next)
        second.next = first

        return second
```
{: .snippet}

## Reference

- [链表理论基础](https://programmercarl.com/%E9%93%BE%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)
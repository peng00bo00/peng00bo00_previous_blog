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
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/RKgLwHR.png" width="80%">
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

本题的暴力解法是先对链表进行遍历从而得到它的大小`sz`然后删除第`sz-n`个节点，这种做法需要对链表进行两次遍历。实际上利用双指针只要一次遍历就可以实现相同的效果：我们首先为链表设置一个哨兵节点`sentinel`并且令`fast`和`slow`两个指针都指向它；然后令快指针`fast`先前进`n+1`步；最后让两个指针同时前进，当`fast`指向`None`时`slow`会指向倒数第`n`个节点的前一个节点，此时只要删除`slow`的下一个节点即可。

使用双指针的算法流程可以参考下图：

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/UG0xBSu.png" width="80%">
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

        for _ in range(n+1):
            fast = fast.next
        
        while fast is not None:
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

翻转链表是链表中的经典问题，我们可以通过修改节点指向来实现：记`cur`为指向当前节点的指针而`pre`为指向`cur`前一个节点的指针，我们只需要利用一个临时指针`tmp`来将当前节点的指向修改为`pre`即可。

整个链表翻转过程可参考下图：

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/6xzxAaV.gif" width="80%">
</div>

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

除了对链表进行遍历外我们还可以使用递归来进行处理：首先对当前头节点`head`的下一个节点`head.next`调用翻转函数，得到翻转的后继链表头节点，记为`newhead`；接着修改后继翻转链表末尾节点的指向，使它指向`head`；然后修改`head`的指向使其指向`None`，这样`head`就称为了翻转后链表的末尾节点；最后返回`newhead`即可。

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

要实现链表中元素两两交换需要每次获取两个节点`first`和`second`然后修改它们的指向。相应地，在更新当前头指针`cur`时需要向后移动2位。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/qN1kx4b.png" width="80%">
</div>

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

递归解法在思维上要更简洁一些：我们同样要获取当前链表的前2个节点`first`和`second`；接着令`first`指向交换后的后续链表；然后令`second`指向`first`，这样就完成了前两个节点的交换；最后返回`second`节点作为当前链表的头节点即可。

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

## 双指针

### 面试题 02.07. 链表相交

给你两个单链表的头节点`headA`和`headB`，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回`null`。

图示两个链表在节点`c1`开始相交：

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/GvrrbR0.png" width="60%">
</div>

题目数据**保证**整个链式结构中不存在环。

注意，函数返回结果后，链表必须**保持其原始结构**。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/cyYQjd7.png" width="60%">
</div>

```
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Intersected at '8'
解释：相交节点的值为 8 （注意，如果两个链表相交则不能为 0）。
从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。
在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/YbhMkxu.png" width="55%">
</div>

```
输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Intersected at '2'
解释：相交节点的值为 2 （注意，如果两个链表相交则不能为 0）。
从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。
在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
```

**示例3：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/nfcXQEI.png" width="35%">
</div>

```
输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。
由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
这两个链表不相交，因此返回 null 。
```

**提示：**

- `listA`中节点数目为`m`。
- `listB`中节点数目为`n`。
- 0 <= `m`, `n` <= 3 * 10⁴。
- 1 <= `Node.val` <= 10⁵。
- 0 <= `skipA` <= `m`。
- 0 <= `skipB` <= `n`。
- 如果`listA`和 `listB`没有交点，`intersectVal`为`0`
- 如果`listA`和 `listB`有交点，`intersectVal` == `listA[skipA + 1]` == `listB[skipB + 1]`

#### Solution

我们假设两个链表的长度分别为`a`和`b`，而公共部分的长度为`c`。这样A和B两个链表在交点前的长度就分别是`a-c`和`b-c`。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/IeaGrxu.png" width="80%">
</div>

我们用两个指针分别对A和B两个链表进行遍历。当A链表的指针走到终点时把它移动到B链表的表头；类似地，当A链表的指针走到终点时把它移动到A链表的表头。当它们都走过`a+b-c`步时恰好会在两个链表的交点处相遇。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/CiwIhrU.png" width="80%">
</div>

[题目链接](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        A, B = headA, headB

        while A != B:
            A = A.next if A else headB
            B = B.next if B else headA
        
        return A
```
{: .snippet}

### 142. 环形链表 II

给定一个链表的头节点`head`，返回链表开始入环的第一个节点。如果链表无环，则返回`null`。

如果链表中有某个节点，可以通过连续跟踪`next`指针再次到达，则链表中存在环。为了表示给定链表中的环，评测系统内部使用整数`pos`来表示链表尾连接到链表中的位置（索引从`0`开始）。如果`pos`是`-1`，则在该链表中没有环。注意：`pos`不作为参数进行传递，仅仅是为了标识链表的实际情况。

**不允许修改**链表。

**示例1：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/R70sKfT.png" width="45%">
</div>

```
输入：head = [3,2,0,-4], pos = 1
输出：返回索引为 1 的链表节点
解释：链表中有一个环，其尾部连接到第二个节点。
```

**示例2：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/8GdM8bK.png" width="22%">
</div>

```
输入：head = [1,2], pos = 0
输出：返回索引为 0 的链表节点
解释：链表中有一个环，其尾部连接到第一个节点。
```

**示例3：**

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/iUX1OVd.png" width="8%">
</div>

```
输入：head = [1], pos = -1
输出：返回 null
解释：链表中没有环。
```

**提示：**

- 链表中节点的数目范围在范围`[0, 10⁴]`内。
- -10⁵ <= `Node.val` <= 10⁵。
- `pos`的值为`-1`或者链表中的一个有效索引。

#### Solution

本题使用双指针时需要让快指针`fast`每次前进2步而慢指针`slow`前进1步，这样当两个指针相遇时快指针`fast`恰好比慢指针`slow`多走了`n`圈，即两个指针重合时`fast`比`slow`多走**环的长度整数倍**。更进一步可以证明此时慢指针`slow`前进的步数为`nb`，而快指针`fast`则前进了`2nb`步，其中`b`为环的长度。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/barkckZ.png" width="80%">
</div>

接下来我们把快指针`fast`移动到链表头，再次让两个指针同时前进，每次都只前进1步。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/Ju6T4IM.png" width="80%">
</div>

当快指针`fast`再次前进了`a`步时，慢指针恰好前进了`a+nb`步，这说明当两个指针再次相遇时的位置就是环的入口。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/DkORLmU.png" width="80%">
</div>

[题目链接](https://leetcode.cn/problems/linked-list-cycle-ii/)：

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        fast, slow = head, head

        while True:
            if fast.next is None or fast.next.next is None:
                return None

            fast = fast.next.next
            slow = slow.next

            if fast == slow:
                break
        
        fast = head

        while fast != slow:
            fast = fast.next
            slow = slow.next
        
        return fast
```
{: .snippet}

## Reference

- [链表理论基础](https://programmercarl.com/%E9%93%BE%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)
- [LeetCode：203.移除链表元素](https://www.bilibili.com/video/BV18B4y1s7R9/?vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：707.设计链表](https://www.bilibili.com/video/BV1FU4y1X7WD/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：206.反转链表](https://www.bilibili.com/video/BV1nB4y1i7eL/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：24.两两交换链表中的节点](https://www.bilibili.com/video/BV1YT411g7br/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：19.删除链表倒数第N个节点](https://www.bilibili.com/video/BV1vW4y1U7Gf/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：142.环形链表II](https://www.bilibili.com/video/BV1if4y1d7ob/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
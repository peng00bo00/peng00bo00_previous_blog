---
layout: article
title: 双指针
key: leetcode-05
clipboard: true
aside:
  toc: true
sidebar:
  nav: LeetCode
---

## 数组

### 27. 移除元素

同[27. 移除元素](/leetcode/2023-01-02-Array.html#27-移除元素)。

#### Solution

[题目链接](https://leetcode.cn/problems/remove-element/)：

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        fast, slow = 0, 0

        for fast in range(len(nums)):
            if nums[fast] != val:
                nums[slow] = nums[fast]
                slow += 1

        return slow
```
{: .snippet}

## 字符串

### 344. 反转字符串

同[344. 反转字符串](/leetcode/2023-01-23-String.html#344-反转字符串)。

#### Solution

[题目链接](https://leetcode.cn/problems/reverse-string/)：

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """

        left, right = 0, len(s)-1

        while left < right:
            s[left], s[right] = s[right], s[left]

            left += 1
            right-= 1
```
{: .snippet}

### 剑指Offer 05.替换空格

同[剑指Offer 05.替换空格](/leetcode/2023-01-23-String.html#剑指offer-05替换空格)。

#### Solution

[题目链接](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)：

```python
class Solution:
    def replaceSpace(self, s: str) -> str:
        N = len(s)

        for i in range(N-1, -1, -1):
            if s[i] == " ":
                s = s[:i] + "%20" + s[i+1:]
        
        return s
```
{: .snippet}

### 151. 反转字符串中的单词

同[151. 反转字符串中的单词](/leetcode/2023-01-23-String.html#151-反转字符串中的单词)。

#### Solution

[题目链接](https://leetcode.cn/problems/reverse-words-in-a-string/)：

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        def removeExtraSpace(s: List[str]) -> List[str]:
            left, right = 0, len(s)-1

            while s[left] == " ":
                left += 1
            
            while s[right] == " ":
                right -= 1
            
            res = []

            while left <= right:
                if s[left] != " ":
                    res.append(s[left])
                    left += 1
                else:
                    while s[left] == " ":
                        left += 1

                    res.append(" ")

            return res
        
        def reverse(s: List[str], left: int, right: int) -> List[str]:
            while left < right:
                s[left], s[right] = s[right], s[left]

                left += 1
                right-= 1
            
            return s
        
        ss = list(s)
        
        ## remove extra space
        ss = removeExtraSpace(ss)

        ## reverse whole list
        ss = reverse(ss, 0, len(ss)-1)

        ## add an additional " " in the end
        ss.append(" ")

        ## reverse each word
        left = right = 0
        for right in range(len(ss)):
            if ss[right] == " ":
                ss = reverse(ss, left, right)
                left = right + 1
        
        ## remove the additional " " in the beginning
        ss = ss[1:]

        return "".join(ss)
```
{: .snippet}

## 链表

### 206. 反转链表

同[206. 反转链表](/leetcode/2023-01-09-LinkedList.html#206反转链表)。

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

### 19. 删除链表的倒数第N个节点

同[19. 删除链表的倒数第N个节点](/leetcode/2023-01-09-LinkedList.html#19-删除链表的倒数第n个结点)。

#### Solution

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

### 面试题 02.07. 链表相交

同[面试题 02.07. 链表相交](/leetcode/2023-01-09-LinkedList.html#面试题-0207-链表相交)。

#### Solution

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

同[142. 环形链表 II](/leetcode/2023-01-09-LinkedList.html#142-环形链表-ii)。

#### Solution

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

## N数之和

### 15. 三数之和

给你一个整数数组`nums`，判断是否存在三元组`[nums[i], nums[j], nums[k]]`满足`i != j`、`i != k`且`j != k`，同时还满足`nums[i] + nums[j] + nums[k] == 0`。请你返回所有和为`0`且不重复的三元组。

**注意：**答案中不可以包含重复的三元组。

**示例1：**

```
输入：nums = [-1,0,1,2,-1,-4]
输出：[[-1,-1,2],[-1,0,1]]
解释：
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0 。
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0 。
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0 。
不同的三元组是 [-1,0,1] 和 [-1,-1,2] 。
注意，输出的顺序和三元组的顺序并不重要。
```

**示例2：**

```
输入：nums = [0,1,1]
输出：[]
解释：唯一可能的三元组和不为 0 。
```

**示例3：**

```
输入：nums = [0,0,0]
输出：[[0,0,0]]
解释：唯一可能的三元组和为 0 。
```

**提示：**

- 3 <= `nums.length` <= 3000。
- -10⁵ <= `nums[i]` <= 10⁵。

#### Solution

三数之和是经典的双指针问题，我们的目标是找到`nums`中不重复的三元组`(nums[i], nums[j], nums[k])`使得它们的和为`0`。由于题目要求是不重复的三元组，我们可以先对`nums`进行排序从而方便去重操作。

本题的基本思路是使用`k`指针对排序后的`nums`进行遍历，然后对`nums[k]`之后的数组使用双指针`i`和`j`进行搜素。根据`nums[k]`的值我们有三种可能的情况：

1. 如果`nums[k] > 0`则说明它后面的元素也都大于`0`，此时无法构造出和为`0`的三元组因此可以直接结束循环
2. 如果`nums[k] == nums[k-1]`则说明遇到了重复的元素，此时向右一定`k`指针继续循环
3. 在其它的情况下需要使用`i`和`j`两个指针对`nums[k]`之后的数组进行搜索

对于需要使用双指针进行搜索的情况，我们令两个指针分别指向后面数组的头和尾，`i = k+1`以及`j = N-1`。此时三个指针分别指向了`nums`数组的不同元素，我们固定`k`指针来分情况讨论：

1. 如果`nums[i] + nums[j] + nums[k] > 0`则需要向左移动`j`指针使得三元组的和变小
2. 如果`nums[i] + nums[j] + nums[k] < 0`则需要向右移动`i`指针使得三元组的和变大
3. 如果`nums[i] + nums[j] + nums[k] == 0`则说明找到了满足要求的一个三元组，将它添加到`res`中并向右向左移动`i`和`j`指针

对于`nums[i] + nums[j] + nums[k] == 0`的情况我们还需要考虑去重。如果发现`nums[i] == nums[i+1]`则需要一直向右移动`i`指针直到它们不相等；类似地，如果发现`nums[j] == nums[j-1]`则需要一直向左移动`j`指针直到它们不相等。

整个算法的时间复杂度为`O(N²)`，代码可参考如下。

[题目链接](https://leetcode.cn/problems/3sum/)：

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums = sorted(nums)
        res  = []

        N = len(nums)

        for k in range(N-2):
            if nums[k] > 0:
                break
            
            if k > 0 and nums[k] == nums[k-1]:
                continue
            
            i = k+1
            j = N-1

            while i < j:
                s = nums[i] + nums[j]
                if s == -nums[k]:
                    res.append([nums[k], nums[i], nums[j]])

                    while i < j and nums[i] == nums[i+1]:
                        i += 1

                    while j > i and nums[j] == nums[j-1]:
                        j -= 1
                    
                    i += 1
                    j -= 1
                
                elif s < -nums[k]:
                    i += 1
                else:
                    j -= 1
        
        return res
```
{: .snippet}

### 18. 四数之和

给你一个由`n`个整数组成的数组`nums`，和一个目标值`target`。请你找出并返回满足下述全部条件且不重复的四元组`[nums[a], nums[b], nums[c], nums[d]]`（若两个四元组元素一一对应，则认为两个四元组重复）：

- `0 <= a, b, c, d < n`
- `a`、`b`、`c`和`d`互不相同
- `nums[a] + nums[b] + nums[c] + nums[d] == target`

你可以按**任意顺序**返回答案。

**示例1：**

```
输入：nums = [1,0,-1,0,-2,2], target = 0
输出：[[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
```

**示例2：**

```
输入：nums = [2,2,2,2,2], target = 8
输出：[[2,2,2,2]]
```

**提示：**

- 1 <= `nums.length` <= 200。
- -10⁹ <= `nums[i]` <= 10⁹。
- -10⁹ <= `target` <= 10⁹。

#### Solution

[题目链接](https://leetcode.cn/problems/4sum/)：

```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums = sorted(nums)
        res = []
        N = len(nums)

        for i in range(N-3):            
            if i > 0 and nums[i] == nums[i-1]:
                continue
            
            for j in range(i+1, N-2):
                if j > i+1 and nums[j] == nums[j-1]:
                    continue
                
                p = j+1
                q = N-1

                while p < q:
                    if nums[i] + nums[j] + nums[p] + nums[q] < target:
                        p += 1
                    elif nums[i] + nums[j] + nums[p] + nums[q] > target:
                        q -= 1
                    else:
                        res.append([nums[i], nums[j], nums[p], nums[q]])

                        while p < q and nums[p] == nums[p+1]:
                            p += 1
                        
                        while p < q and nums[q] == nums[q-1]:
                            q -= 1

                        p += 1
                        q -= 1
        
        return res
```
{: .snippet}

## Reference

- [LeetCode：27.移除元素](https://www.bilibili.com/video/BV12A4y1Z7LP/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：344.反转字符串](https://www.bilibili.com/video/BV1fV4y17748/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：151.翻转字符串里的单词](https://www.bilibili.com/video/BV1uT41177fX/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：206.反转链表](https://www.bilibili.com/video/BV1nB4y1i7eL/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：19.删除链表倒数第N个节点](https://www.bilibili.com/video/BV1vW4y1U7Gf/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：142.环形链表II](https://www.bilibili.com/video/BV1if4y1d7ob/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：15.三数之和](https://www.bilibili.com/video/BV1GW4y127qo/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：18.四数之和](https://www.bilibili.com/video/BV1DS4y147US/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
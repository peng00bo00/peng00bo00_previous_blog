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

        for i, char in enumerate(s[::-1]):
            if char == " ":
                s = s[:N-(i+1)] + "%20" + s[N-i:]
        
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
        def removeSpace(s_list: List[str]) -> List[str]:
            left, right = 0, len(s_list)-1

            while s_list[left] == " ":
                left += 1
            
            while s_list[right] == " ":
                right -= 1
            
            ret = []

            while left <= right:
                if s_list[left] != " ":
                    ret.append(s_list[left])
                    left += 1
                else:
                    while s_list[left] == " ":
                        left += 1

                    ret.append(" ")

            return ret
        
        def reverse(s_list: List[str]) -> List[str]:
            left, right = 0, len(s_list)-1

            while left < right:
                s_list[left], s_list[right] = s_list[right], s_list[left]

                left += 1
                right-= 1

            return s_list

        s_list = list(s)

        ## remove extra spaces
        s_list = removeSpace(s_list)

        ## reverse the whole string
        s_list = reverse(s_list)

        ## reverse each word
        fast, slow = 0, 0
        s_list.append(" ")

        for fast in range(len(s_list)):
            if s_list[fast] != " ":
                continue
            
            s_list[slow: fast] = reverse(s_list[slow: fast])

            slow = fast+1

        s_list.pop()

        return "".join(s_list)
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
- -10<sup>5</sup> <= `nums[i]` <= 10<sup>5</sup>。

#### Solution

[题目链接](https://leetcode.cn/problems/3sum/)：

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums, res = sorted(nums), []
        N = len(nums)

        for i in range(N-2):
            if nums[i] > 0:
                break
            
            if i > 0 and nums[i] == nums[i-1]:
                continue

            left, right = i+1, N-1
            while left < right:
                if nums[i] + nums[left] + nums[right] == 0:
                    res.append([nums[i], nums[left], nums[right]])

                    while left < right and nums[left] == nums[left+1]:
                        left += 1
                    
                    while right > left and nums[right] == nums[right-1]:
                        right -= 1
                
                if nums[i] + nums[left] + nums[right] < 0:
                    left += 1
                else:
                    right -= 1

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
- -10<sup>9</sup> <= `nums[i]` <= 10<sup>9</sup>。
- -10<sup>9</sup> <= `target` <= 10<sup>9</sup>。

#### Solution

[题目链接](https://leetcode.cn/problems/4sum/)：

```python
class Solution:
    def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
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
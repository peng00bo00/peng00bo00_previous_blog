---
layout: article
title: 栈与队列
key: leetcode-06
clipboard: true
aside:
  toc: true
sidebar:
  nav: LeetCode
---

## 栈

### 232. 用栈实现队列

请你仅使用两个栈实现先入先出队列。队列应当支持一般队列支持的所有操作（`push`、`pop`、`peek`、`empty`）：

实现`MyQueue`类：

- `void push(int x)`将元素`x`推到队列的末尾
- `int pop()`从队列的开头移除并返回元素
- `int peek()`返回队列开头的元素
- `boolean empty()`如果队列为空，返回`true`；否则，返回`false`

**说明：**

- 你**只能**使用标准的栈操作 — 也就是只有`push to top`,`peek/pop from top`,`size`,和`is empty`操作是合法的。
- 你所使用的语言也许不支持栈。你可以使用`list`或者`deque`（双端队列）来模拟一个栈，只要是标准的栈操作即可。

**示例1：**

```
输入：
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
输出：
[null, null, null, 1, 1, false]

解释：
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
```

**提示：**

- 1 <= `x` <= 9。
- 最多调用`100`次`push`、`pop`、`peek`和`empty`。
- 假设所有操作都是有效的（例如，一个空的队列不会调用`pop`或者`peek`操作）。

#### Solution

[题目链接](https://leetcode.cn/problems/implement-queue-using-stacks/)：

```python
class MyQueue:

    def __init__(self):
        self.stack_in = []
        self.stack_out= []

    def push(self, x: int) -> None:
        self.stack_in.append(x)

    def pop(self) -> int:
        if self.stack_out:
            return self.stack_out.pop()
        else:
            while self.stack_in:
                self.stack_out.append(self.stack_in.pop())
            
            return self.stack_out.pop()

    def peek(self) -> int:
        x = self.pop()
        self.stack_out.append(x)

        return x

    def empty(self) -> bool:
        return not (self.stack_in or self.stack_out)


# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```
{: .snippet}

### 20. 有效的括号

给定一个只包括`'('`，`')'`，`'{'`，`'}'`，`'['`，`']'`的字符串`s`，判断字符串是否有效。

有效字符串需满足：

- 左括号必须用相同类型的右括号闭合。
- 左括号必须以正确的顺序闭合。
- 每个右括号都有一个对应的相同类型的左括号。

**示例1：**

```
输入：s = "()"
输出：true
```

**示例2：**

```
输入：s = "()[]{}"
输出：true
```

**示例3：**

```
输入：s = "(]"
输出：false
```

**提示：**

- 1 <= `s.length` <= 10⁴。
- s 仅由括号`'()[]{}'`组成。

#### Solution

[题目链接](https://leetcode.cn/problems/valid-parentheses/)：

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []

        for char in s:
            if char == "(":
                stack.append(")")
            elif char == "[":
                stack.append("]")
            elif char == "{":
                stack.append("}")
            elif len(stack) == 0 or char != stack[-1]:
                return False
            else:
                stack.pop()
        
        return len(stack) == 0
```
{: .snippet}

## 队列

### 225. 用队列实现栈

请你仅使用两个队列实现一个后入先出（LIFO）的栈，并支持普通栈的全部四种操作（`push`、`top`、`pop`和`empty`）。

实现`MyStack`类：

- `void push(int x)`将元素`x`压入栈顶。
- `int pop()`移除并返回栈顶元素。
- `int top()`返回栈顶元素。
- `boolean empty()`如果栈是空的，返回`true`；否则，返回`false`。

**注意：**

- 你只能使用队列的基本操作 — 也就是`push to back`、`peek/pop from front`、`size`和`is empty`这些操作。
- 你所使用的语言也许不支持队列。你可以使用`list`（列表）或者`deque`（双端队列）来模拟一个队列, 只要是标准的队列操作即可。

**示例1：**

```
输入：
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
输出：
[null, null, null, 2, 2, false]

解释：
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // 返回 2
myStack.pop(); // 返回 2
myStack.empty(); // 返回 False
```

**提示：**

- 1 <= `x` <= 9。
- 最多调用`100`次`push`、`pop`、`peek`和`empty`。
- 每次调用`pop`和`top`都保证栈不为空。

#### Solution

[题目链接](https://leetcode.cn/problems/implement-stack-using-queues/)：

```python
from collections import deque

class MyStack:

    def __init__(self):
        self.queue_in = deque()
        self.queue_out= deque()

    def push(self, x: int) -> None:
        self.queue_in.append(x)

    def pop(self) -> int:
        for i in range(len(self.queue_in) - 1):
            self.queue_out.append(self.queue_in.popleft())
        
        self.queue_in, self.queue_out = self.queue_out, self.queue_in

        return self.queue_out.popleft()

    def top(self) -> int:
        return self.queue_in[-1]

    def empty(self) -> bool:
        return len(self.queue_in) == 0


# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```
{: .snippet}

```python
from collections import deque

class MyStack:

    def __init__(self):
        self.queue = deque()

    def push(self, x: int) -> None:
        self.queue.append(x)

    def pop(self) -> int:
        for i in range(len(self.queue)-1):
            self.queue.append(self.queue.popleft())
        
        return self.queue.popleft()

    def top(self) -> int:
        return self.queue[-1]

    def empty(self) -> bool:
        return len(self.queue) == 0


# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```
{: .snippet}


## Reference

- [栈与队列理论基础](https://programmercarl.com/%E6%A0%88%E4%B8%8E%E9%98%9F%E5%88%97%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)
- [LeetCode：232.用栈实现队列](https://www.bilibili.com/video/BV1nY4y1w7VC/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：225.用队列实现栈](https://www.bilibili.com/video/BV1Fd4y1K7sm/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
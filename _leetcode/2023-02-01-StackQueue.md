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

使用两个栈来实现队列时我们需要定义一个**输入栈**`stack_in`和一个**输出栈**`stack_out`。这样队列的操作就可以按照如下方法实现：

- `push`：直接向输入栈`stack_in`添加元素；
- `pop`：如果输出栈`stack_out`非空则直接`pop`，否则把输入栈`stack_in`中的元素依次弹出到输出栈`stack_out`中再从输出栈`pop`；
- `peek`：调用定义好的`pop`函数弹出元素，然后再把它加入到输出栈`stack_out`中；
- `empty`：检查输入栈`stack_in`和输出栈`stack_out`是否均为空。

队列操作过程可以参考下图。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/https://pic.leetcode-cn.com/1614908055-DRhjRN-232.gif">
</div>

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

括号匹配是栈的经典应用。对于`s`中的每个字符`char`，如果`char`是一个左括号则把对应的右括号压入栈`stack`中，否则需要检查`stack`：

- 如果发现栈为空则说明`char`是多余的反括号，直接返回`False`；
- 如果`char`与栈顶元素不相同说明括号匹配失败，直接返回`False`；
- 如果`char`与栈顶元素相同说明括号匹配成功，弹出`stack`中的元素继续进行匹配。

完成对`s`的遍历后再检查`stack`是否为空即可。如果`stack`非空说明还有括号需要匹配，返回`False`；否则返回`True`。

整个匹配过程可以参考如下。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/2noJagb.gif">
</div>

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

### 1047. 删除字符串中的所有相邻重复项

给出由小写字母组成的字符串`s`，**重复项删除操作**会选择两个相邻且相同的字母，并删除它们。

在`s`上反复执行重复项删除操作，直到无法继续删除。

在完成所有重复项删除操作后返回最终的字符串。答案保证唯一。

**示例：**

```
输入："abbaca"
输出："ca"
解释：
例如，在 "abbaca" 中，我们可以删除 "bb" 由于两字母相邻且相同，这是此时唯一可以执行删除操作的重复项。之后我们得到字符串 "aaca"，其中又只有 "aa" 可以执行重复项删除操作，所以最后的字符串为 "ca"。
```

**提示：**

- 1 <= `s.length` <= 20000。
- `s`仅由小写英文字母组成。

#### Solution

[题目链接](https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/)：

```python
class Solution:
    def removeDuplicates(self, s: str) -> str:
        stack = []
        for char in s:
            if not stack or char != stack[-1]:
                stack.append(char)
            else:
                stack.pop()
            
        return "".join(stack)
```
{: .snippet}

```python
class Solution:
    def removeDuplicates(self, s: str) -> str:
        ss = list(s)
        slow = 0

        for fast in range(len(ss)):
            ss[fast], ss[slow] = ss[slow], ss[fast]

            if slow > 0 and ss[slow] == ss[slow-1]:
                slow -= 1
            else:
                slow += 1
            
        return "".join(ss[:slow])
```
{: .snippet}

### 150. 逆波兰表达式求值

给你一个字符串数组`tokens`，表示一个根据**逆波兰表示法**表示的算术表达式。

请你计算该表达式。返回一个表示表达式值的整数。

**注意：**

- 有效的算符为`'+'`、`'-'`、`'*'`和`'/'`。
- 每个操作数（运算对象）都可以是一个整数或者另一个表达式。
- 两个整数之间的除法总是**向零截断**。
- 表达式中不含除零运算。
- 输入是一个根据逆波兰表示法表示的算术表达式。
- 答案及所有中间计算结果可以用**32 位**整数表示。

**示例1：**

```
输入：tokens = ["2","1","+","3","*"]
输出：9
解释：该算式转化为常见的中缀算术表达式为：((2 + 1) * 3) = 9
```

**示例2：**

```
输入：tokens = ["4","13","5","/","+"]
输出：6
解释：该算式转化为常见的中缀算术表达式为：(4 + (13 / 5)) = 6
```

**示例3：**

```
输入：tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
输出：22
解释：该算式转化为常见的中缀算术表达式为：
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```

**提示：**

- 1 <= `tokens.length` <= 10⁴。
- `tokens[i]`是一个算符（`"+"`、`"-"`、`"*"`或`"/"`），或是在范围`[-200, 200]`内的一个整数。

**逆波兰表达式：**

逆波兰表达式是一种后缀表达式，所谓后缀就是指算符写在后面。

- 平常使用的算式则是一种中缀表达式，如`( 1 + 2 ) * ( 3 + 4 )`。
- 该算式的逆波兰表达式写法为`( ( 1 2 + ) ( 3 4 + ) * )`。

逆波兰表达式主要有以下两个优点：

- 去掉括号后表达式无歧义，上式即便写成 `1 2 + 3 4 + * `也可以依据次序计算出正确结果。
- 适合用栈操作运算：遇到数字则入栈；遇到算符则取出栈顶两个数字进行计算，并将结果压入栈中。

#### Solution

[题目链接](https://leetcode.cn/problems/evaluate-reverse-polish-notation/)：

```python
from operator import add, sub, mul

class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        ops = {"+": add, "-": sub, "*": mul, "/": lambda x, y: int(x/y)}
        stack = []

        for token in tokens:
            if token not in ops:
                stack.append(int(token))
            else:
                y = stack.pop()
                x = stack.pop()
                
                stack.append(ops[token](x, y))
        
        return stack.pop()
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

本题与[用栈实现队列](/leetcode/2023-02-01-StackQueue.html#232-用栈实现队列)的主要区别在于把**输入队列**`queue_in`中的元素依次输出到**输出队列**`queue_out`中并不能实现队列中元素的逆序。因此本题中输出队列`queue_out`更多地是作为输入队列`queue_in`的备份，大多数操作只需要利用`queue_in`即可实现：

- `push`：直接向输入队列`queue_in`添加元素；
- `pop`：把输入队列`queue_in`中的元素依次输入到输出队列`queue_out`中直到只剩最后一个，然后交换两个队列的指针并最后从输出队列`queue_out`弹出剩余元素；
- `top`：返回输入队列`queue_in`中最后一个元素；
- `empty`：检查输入队列`queue_in`是否为空。

整个操作过程可以参考下图。

<div align=center>
<img src="https://pic1.xuehuaimg.com/proxy/i.imgur.com/dmUTn3Z.gif">
</div>

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

如果使用双向队列`deque`则栈的实现会更加简单，代码可参考如下：

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

### 239. 滑动窗口最大值

给你一个整数数组`nums`，有一个大小为`k`的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的`k`个数字。滑动窗口每次只向右移动一位。

返回**滑动窗口中的最大值**。

**示例1：**

```
输入：nums = [1,3,-1,-3,5,3,6,7], k = 3
输出：[3,3,5,5,6,7]
解释：
滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**示例2：**

```
输入：nums = [1], k = 1
输出：[1]
```

**提示：**

- 1 <= `nums.length` <= 10⁵。
- -10⁴ <= `nums[i]` <= 10⁴。
- 1 <= `k` <= `nums.length`。

#### Solution

[题目链接](https://leetcode.cn/problems/sliding-window-maximum/)：

```python
from collections import deque

class MyQueue:
    def __init__(self):
        self.queue = deque()
    
    def pop(self, x:int) -> None:
        if self.queue and x == self.queue[0]:
            self.queue.popleft()
    
    def push(self, x: int) -> None:
        while self.queue and x > self.queue[-1]:
            self.queue.pop()
        
        self.queue.append(x)

    def front(self) -> int:
        return self.queue[0]

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        queue = MyQueue()
        res = []

        for i in range(k):
            queue.push(nums[i])
        
        res.append(queue.front())

        for i in range(k, len(nums)):
            queue.pop(nums[i-k])
            queue.push(nums[i])
            res.append(queue.front())
        
        return res
```
{: .snippet}

### 347. 前K个高频元素

给你一个整数数组`nums`和一个整数`k`，请你返回其中出现频率前`k`高的元素。你可以按**任意顺序**返回答案。

**示例1：**

```
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```

**示例2：**

```
输入: nums = [1], k = 1
输出: [1]
```

**提示：**

- 1 <= `nums.length` <= 10⁵。
- `k`的取值范围是`[1, 数组中不相同的元素的个数]`。
- 题目数据保证答案唯一，换句话说，数组中前`k`个高频元素的集合是唯一的。

#### Solution

[题目链接](https://leetcode.cn/problems/top-k-frequent-elements/)：

```python
import heapq

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = {}
        for x in nums:
            count[x] = count.get(x, 0) + 1
        
        heap = []

        for x, freq in count.items():
            heapq.heappush(heap, (freq, x))

            if len(heap) > k:
                heapq.heappop(heap)
        
        res = [0 for _ in range(k)]
        for i in range(k-1, -1, -1):
            res[i] = heapq.heappop(heap)[1]

        return res
```
{: .snippet}


## Reference

- [栈与队列理论基础](https://programmercarl.com/%E6%A0%88%E4%B8%8E%E9%98%9F%E5%88%97%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)
- [LeetCode：232.用栈实现队列](https://www.bilibili.com/video/BV1nY4y1w7VC/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：225.用队列实现栈](https://www.bilibili.com/video/BV1Fd4y1K7sm/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：20.有效的括号](https://www.bilibili.com/video/BV1AF411w78g/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：1047.删除字符串中的所有相邻重复项](https://www.bilibili.com/video/BV12a411P7mw/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：150.逆波兰表达式求值](https://www.bilibili.com/video/BV1kd4y1o7on/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：239.滑动窗口最大值](https://www.bilibili.com/video/BV1XS4y1p7qj/?spm_id_from=333.788&vd_source=7a2542c6c909b3ee1fab551277360826)
- [LeetCode：347.前K个高频元素](https://www.bilibili.com/video/BV1Xg41167Lz/?vd_source=7a2542c6c909b3ee1fab551277360826)
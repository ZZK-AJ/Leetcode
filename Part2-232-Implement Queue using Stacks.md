## 题目

Implement实现 the following operations操作 of a queue队列 using stacks堆栈.

- push(x) -- Push element x to the back of queue.
- pop() -- Removes the element from in front of queue.
- peek() -- Get the front element.
- empty() -- Return whether the queue is empty.

**Example:**

```
MyQueue queue = new MyQueue();

queue.push(1);
queue.push(2);  
queue.peek();  // returns 1
queue.pop();   // returns 1
queue.empty(); // returns false
```

**Notes:**

- You must use *only* standard operations of a stack -- which means only `push to top`, `peek/pop from top`, `size`, and `is empty` operations are valid.您必须仅使用堆栈的标准操作 - 这意味着只能从顶部切换到顶部，查看/弹出，大小，并且空操作是有效的。
- Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard operations of a stack.根据您的语言，本机可能不支持堆栈。您可以使用列表或双端队列（双端队列）来模拟堆栈，只要您只使用堆栈的标准操作即可。
- You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).您可以假设所有操作都是有效的（例如，不会在空队列上调用pop或Peek操作）。

## 思路

利用两个堆栈，一个叫输入栈，一个叫输出栈。用于实现进入队列Push(x)，出队列pop()，查看最后一个元素peek()，及判断是否为空empty()函数。每次从输入栈进，输出栈出。

push操作：将加入的元素添加到输入栈；

pop操作：从输出栈取走元素，输出栈没有元素时，将输入栈元素依次出栈压入输出栈，再从输出栈取出；

peek操作：同pop操作原理一样；

empty为真的条件是两个栈都为空。



## 解法(Python)

```python
class MyQueue:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.stackin = []
        self.stackout = []
        
    def push(self, x: int) -> None:
        """
        Push element x to the back of queue.
        """
        self.stackin.append(x)

    def pop(self) -> int:
        """
        Removes the element from in front of queue and returns that element.
        """
        if not self.stackout:  # 当输出栈没有元素的时候，遍历读入输入栈
            while self.stackin:  # 倒序压入输出栈
                a = self.stackin.pop()
                self.stackout.append(a)
        return self.stackout.pop()

    def peek(self) -> int:
        """
        Get the front element.
        """
        if not self.stackout:
            while self.stackin:
                a = self.stackin.pop()
                self.stackout.append(a)
        return self.stackout[-1]  

    def empty(self) -> bool:
        """
        Returns whether the queue is empty.
        """
        if not self.stackin and not self.stackout:
            return True
        else:
            return False


# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```


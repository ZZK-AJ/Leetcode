## 题目

Given a linked list, return the node where the cycle begins.返回环开始的那个节点 If there is no cycle, return null.没环的话，就返回null

To represent表示 a cycle in the given linked list, we use an integer整数 pos which represents the position位置 (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.

Note: Do not modify the linked list.

**Example 1:**

```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

**Example 2:**

```
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

**Example 3:**

```
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
```

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

 

**Follow up**:
Can you solve it without using extra space?

## 思路

1. 把见过的节点丢集合里，下次再遇见就是环的开始(疑问，这里不能链表有重复元素吗？？？)

   ```python
   # Definition for singly-linked list.
   # class ListNode(object):
   #     def __init__(self, x):
   #         self.val = x
   #         self.next = None
   
   class Solution(object):
       def detectCycle(self, head):
           """
           :type head: ListNode
           :rtype: ListNode
           """
           s = {None}
           while head not in s:
               s.add(head)
               head = head.next
           return head
   ```

2. 使用快慢指针的方法，一个纯数学的解法

   设环的起始节点为 E，快慢指针从 head 出发，快指针速度为 2，设相交节点为 X，head 到 E 的距离为 H，E 到 X 的距离为 D，环的长度为 L，那么有：快指针走过的距离等于慢指针走过的距离加快指针多走的距离（多走了 n 圈的 L） `2(H + D) = H + D + nL`，因此可以推出 `H = nL - D`，这意味着如果我们让俩个慢指针一个从 head 出发，一个从 X 出发的话，他们一定会在节点 E 相遇

   ```python
   					        _____
   				         /     \
    head___________E       \
   				        \       /
   				         X_____/ 
   ```

```python
class Solution(object):
    def detectCycle(self, head):
        slow = fast = head
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
            if slow == fast:
                break
        else:
            return None
        while head is not slow:
            head = head.next
            slow = slow.next
        return head
```


[TOC]

### 题目

Given a linked list, swap交换 every two adjacent相邻的 nodes and return its head.

You may **not** modify the values in the list's nodes, only nodes itself may be changed.

**Example:**

```
Given 1->2->3->4, you should return the list as 
			2->1->4->3.
```

### 思路：

和链表反转类似，关键在于

有三个指针，分别指向前后和当前节点。不同点是两两交换后，移动节点步长为２

### python解法(还有瑕疵，后续改进)

```python
"""
Given 1->2->3->4, you should return the list as
     2->1->4->3.
要理解，需求是两两互换位置，也就是说，本来 1.next->2 2.next->3 调换后 2.next->1 1.next->3
pre pre.next pre.next.next 会变成
pre.next.next->pre pre.next->pre.next.next

1->2->3->4
经过第一次循环
2->1->3->4
第二次循环，1为pre不变，
2->1->4->3

"""

class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        pre, pre.next = self, head
        while pre.next and pre.next.next:
            a = pre.next  # a为当前节点
            b = a.next  # b为a的后一个节点

            pre.next = b  # 把后一个节点设为当前节点，用于下次
            b.next = a  # 这里实现了调换，这里把b放到了当前节点位置
            a.next = b.next  # 实现a的下一个节点，调整为最后一个节点
            # pre.next, b.next, a.next = b,a,b.next
            pre = a  # 最后a作为pre当前前一个节点，用于后续循环，后续每次循环中pre是不处理的，这样子实现两两互换后，下一个两两互换
        return self.next

if __name__ == "__main__":
    l1_list = [1, 2, 3, 4]

    l1 = ListNode(0)
    l1_copy = l1
    for l1_index in l1_list:
        l1_copy.next = ListNode(l1_index)
        l1_copy = l1_copy.next

    for i in range(len(l1_list)+1):
        print(l1.val)
        print(l1.next)
        l1 = l1.next

    print('---'*13)
    final_ln = Solution().swapPairs(l1)
    print(final_ln)
```

### Java解法

后续补充！


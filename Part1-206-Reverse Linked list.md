[TOC]

## 题目

Reverse 反转 a singly linked list 单向链表.

**Example:**

```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

**Follow up:**

A linked list can be reversed either iteratively 迭代 or recursively 递归. Could you implement both 应用这两种方法?

## 思路

### 方法1：迭代

假设存在链表          1 → 2 → 3 → Ø

要把它改成     Ø ← 1 ← 2 ← 3 

这样子对齐后，就能够明白对传入的每一个元素的操作

在遍历列表时，将当前节点的 next 指针改为指向前一个元素（第一个元素1的时候就指向None）。

由于节点没有引用其上一个节点，因此必须事先用一个临时变量存储其前一个元素。

在更改引用之前，还需要另一个指针来存储下一个节点。不要忘记在最后返回新的头引用！

**复杂度分析**

- 时间复杂度：O(n)*，假设 n* 是列表的长度，时间复杂度是 O(n)
- 空间复杂度：O(1)

### 方法2：递归

![image-20190515184912018](/Users/zzk/Library/Application Support/typora-user-images/image-20190515184912018.png)

n_{k}.next.next = n_{k}

其实 n_{k}.next 就是  n_{k+1}.next = n{k}就相当于反转了

```java
public ListNode reverseList(ListNode head) {
    if (head == null || head.next == null) return head;
    ListNode p = reverseList(head.next);
    head.next.next = head;		// 这一步实现反转
    head.next = null;
    return p;
}
```



## Python版解法

```python
"""
假设存在链表      1  → 2  → 3 → Ø
要把它改成   Ø ← 1 ← 2 ← 3
"""


class ListNode:
    def __init__(self, x):
        self.val = x
        self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        cur = head
        prev = None
        while cur:
            cur.next = prev     # 把当前元素的next指向前一个
            prev = cur      # 把当前这个元素设为prev，为下一次做准备
            cur = cur.next      # 把原来元素的下一个设为当前这个元素，为下一次做准备，继续循环
        return prev     # 最后返回最前面一个的元素，完成反转


if __name__ == "__main__":
    l1_list = [9, 4, 3]     # 创建两个列表

    l1 = ListNode(None)        # 初始化l1,第一个值为0，None其实也可以的
    l1_copy = l1        # 这里要用l1_copy含义是因为要对后面利用l1_copy不断创建值赋值，不能用最初的l1
    # print(l1_copy)
    for l1_index in l1_list:
        l1_copy.next = ListNode(l1_index)   # 这里可以看出，下一个里面存着一个ListNode对象，在下一次循环给它赋值
        # print(l1_copy)
        # print(l1_copy.next)
        l1_copy = l1_copy.next   # 这里都是用来了l1_copy，为什么后面用l1.next,因为l1和l1_copy都指向同一个对象
        # print(l1_copy)
        # print('===')

    for i in range(len(l1_list)):
        print(l1.val)       # 第一个是None
        print(l1.next)
        l1 = l1.next        # 这样子把next指向的对象赋给当前，就可以得到下一个的值，从而迭代出这个数据结构

    final_ln = Solution().reverseList(l1)

    for i in range(len(l1_list)):
        if final_ln == None:
            pass
        else:
            print(final_ln.val)       # 第一个是None
            print(final_ln.next)
            final_ln = final_ln.next        # 这样子把next指向的对象赋给当前，就可以得到下一个的值，从而迭代出这个数据结构

```



## Java版解法

```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null;  
    ListNode curr = head;
    while (curr != null) {    //当前值有就一直循环
        ListNode nextTemp = curr.next;  // 保存的下一个先暂存起来
        curr.next = prev;  // 前一个先设为下一个，实现反转
        prev = curr;  // 反转，当然现在的值要设为前一个的值
        curr = nextTemp;  //最后把之前暂存的下一个设为当前值，进行下一次运算
    }
    return prev;
}
```














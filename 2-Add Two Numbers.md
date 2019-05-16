[TOC]

### 题目

You are given two **non-empty** linked lists(两个 **非空** 的链表) representing(表示) two non-negative(非负) integers（整数）.

 The digits are stored in **reverse order** and each of their nodes contain a single digit（一位数字）. Add the two numbers and return it as a linked list.

You may assume(假设) the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

### 思路

使用变量来代表进位，并从包含最低有效位的链表头开始模拟逐位相加的过程

![image-20190513160104615](/Users/zzk/Library/Application Support/typora-user-images/image-20190513160104615.png)

从最低有效位开始相加，计算两个数字的和时可能出现进位的情况，所以把进位carry设为1

伪代码如下：

- 将当前结点初始化为返回列表的哑结点。
- 将进位 *carry* 初始化为 0。
- 将 *p* 和 *q* 分别初始化为列表 l1*l*1 和 l2*l*2 的头部。
- 遍历列表 *l*1和 *l*2直至到达它们的尾端。
  - 将 *x* 设为结点 p*p* 的值。如果 *p* 已经到达 l1*l*1 的末尾，则将其值设置为 0。
  - 将 y*y* 设为结点 q*q* 的值。如果 q*q* 已经到达 l2*l*2 的末尾，则将其值设置为 0。
  - 设定 sum = x + y + carry。
  - 更新进位的值，carry = sum / 10。
  - 创建一个数值为 (sum mod 10) 的新结点，并将其设置为当前结点的下一个结点，然后将当前结点前进到下一个结点。
  - 同时，将 *p* 和 *q* 前进到下一个结点。
- 检查 carry = 1是否成立，如果成立，则向返回列表追加一个含有数字 11 的新结点。
- 返回哑结点的下一个结点。



### Java版本

```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode dummyHead = new ListNode(0);
    ListNode p = l1, q = l2, curr = dummyHead;
    int carry = 0;
    while (p != null || q != null) {
        int x = (p != null) ? p.val : 0;
        int y = (q != null) ? q.val : 0;
        int sum = carry + x + y;
        carry = sum / 10;
        curr.next = new ListNode(sum % 10);
        curr = curr.next;
        if (p != null) p = p.next;
        if (q != null) q = q.next;
    }
    if (carry > 0) {
        curr.next = new ListNode(carry);
    }
    return dummyHead.next;
}
```

复杂度分析

时间复杂度：O(max(m, n))，假设 m 和 n 分别表示 l1 和 l2 的长度，上面的算法最多重复 max(m, n)次。

空间复杂度：O(max(m,n))， 新列表的长度最多为 max(m,n)+1。

### python版本

```python
class Solution(object):
    # 直接对两个链表操作；对应节点上的值做加法运算，过10则进位。位数不够则补0
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        l = ListNode(0)     # l为最后保存结果的
        l_copy = l
        carry = 0       # 定义两数相加是否大于10进位
        while l1 or l2:
            # 因为l1与l2链表对应的位数可能不同，此时需要将空缺的位置补0
            l1_val = l1.val if l1 else 0
            l2_val = l2.val if l2 else 0
            two_sum = l1_val + l2_val + carry
            if two_sum < 10:        # 小于10，不进位的情况下
                l_copy.next = ListNode(two_sum)
                carry = 0
            else:
                carry = 1     # 否则进位数就是和10整除的得数，其实就是0或1，可以直接1
                l_copy.next = ListNode(two_sum%10)      # 把对应的余数放到 ListNode
            l_copy = l_copy.next
            l1 = l1.next if l1 else None    # 这里把next保存的对象设为新的l1和l2
            l2 = l2.next if l2 else None    # 只要l1和l2中有一个还有下个值就要继续while循环
        if carry > 0:       # 为什么在这里判断carry？是最后一次相加之后，有carry的话就要进位
            l_copy.next = ListNode(carry)
        return l.next


if __name__ == "__main__":
    l1_list = [9, 4, 3]     # 创建两个列表
    l2_list = [5, 6, 4]

    l1 = ListNode(0)        # 初始化l1
    l1_copy = l1        # 这里为什么要用l1_copy才能构造出
    for l1_index in l1_list:
        l1_copy.next = ListNode(l1_index)   # 这里可以看出，下一个里面存着一个ListNode对象，在下一次循环给它赋值
        l1_copy = l1_copy.next   # 这里都是用来了l1_copy，为什么后面用l1.next,因为l1和l1_copy都指向同一个对象

    l2 = ListNode(0)
    l2_copy = l2
    for l2_index in l2_list:
        l2_copy.next = ListNode(l2_index)
        l2_copy = l2_copy.next

    final_listnode = Solution().addTwoNumbers(l1.next, l2.next)
    print('---'*13)
    print(final_listnode.val)
    print(final_listnode.next)
```



![image-20190513190947131](/Users/zzk/Library/Application Support/typora-user-images/image-20190513190947131.png)



![image-20190513190952715](/Users/zzk/Library/Application Support/typora-user-images/image-20190513190952715.png)


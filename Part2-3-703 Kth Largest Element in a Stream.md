## 题目

Design a class to find the **k**th largest element in a stream. Note that it is the kth largest element in the sorted order, not the kth distinct element.

设计一个类来查找流中第k个最大元素。请注意，它是排序顺序中的第k个最大元素，而不是第k个不同元素。

Your `KthLargest` class will have a constructor which accepts an integer `k` and an integer array `nums`, which contains initial elements from the stream. 

你的KthLargest类将有一个构造函数，它接受一个整数k和一个整数数组nums，它包含来自流的初始元素。

For each call to the method `KthLargest.add`, return the element representing the kth largest element in the stream.

对于方法KthLargest.add的每次调用，返回表示流中第k个最大元素的元素。

**Example:**

```
int k = 3;
int[] arr = [4,5,8,2];
KthLargest kthLargest = new KthLargest(3, arr);
kthLargest.add(3);   // returns 4
kthLargest.add(5);   // returns 5
kthLargest.add(10);  // returns 5
kthLargest.add(9);   // returns 8
kthLargest.add(4);   // returns 8
```

**Note:** 
You may assume that `nums`' length ≥ `k-1` and `k` ≥ 1.



## 解法：

方法一：

直接降序排序，然后取第k个元素返回，add时每次都再排序一次，这样时间复杂度为O(k*logk)

```python
# 1.直接排序
class KthLargest:
    def __init__(self, k: int, nums: List[int]):
        self.nums = nums
        self.k = k
        self.nums.sort(reverse = True)
        while len(self.nums) > k:
            self.nums.pop()

    def add(self, val: int) -> int:
        self.nums.append(val)
        self.nums.sort(reverse = True)
        if len(self.nums) > self.k:  # 只要大于k个，就剔除，最后就只需返回倒序的最后一个就行
            self.nums.pop()
        return self.nums[-1]
```



方法二：

使用小顶堆实现的优先队列，Python 中标准库 heapq 就是小顶堆，时间复杂度降低为`O(k)`

```python
# 2.小顶堆，二叉树形式，根节点为最小
import heapq
class KthLargest:
    def __init__(self, k: int, nums: List[int]):
        self.pool = nums
        heapq.heapify(self.pool)
        self.k = k
        while len(self.pool) > k:
            heapq.heappop(self.pool)

    def add(self, val: int) -> int:
        if len(self.pool) < self.k:
            heapq.heappush(self.pool, val)
        elif val > self.pool[0]:
            heapq.heapreplace(self.pool, val)
        return self.pool[0]
```



Java 版解法：

维护一个最小堆，堆的元素个数为常量 k，新加入一个元素和堆顶比较，如果比堆顶元素小，丢弃，否则删除堆顶元素，插入新元素。

```Java
class KthLargest {
    final PriorityQueue<Integer> q ;
    final int k;
    public KthLargest(int k, int[] nums) {
        this.k = k;
        q = new PriorityQueue<Integer>(k);
        for(int i: nums) {
            add(i);
        }
    }
    
    public int add(int val) {
        if(q.size() < k) {
            q.offer(val);
            
        }
        else if(q.peek() < val) {
            q.poll();
            q.offer(val);
        }
        return q.peek();
    }
}
```


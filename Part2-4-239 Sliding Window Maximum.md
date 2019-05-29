## 题目

Given an array *nums*, there is a sliding window of size *k* which is moving from the very left of the array to the very right. You can only see the *k* numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

**Example:**

```
Input: nums = [1,3,-1,-3,5,3,6,7], and k = 3
Output: [3,3,5,5,6,7] 
Explanation: 

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**Note:** 
You may assume *k* is always valid, 1 ≤ k ≤ input array's size for non-empty array.

**Follow up:**
Could you solve it in linear time?



## 解法

使用双端队列

```python
import collections
class Solution(object):
    def maxSlidingWindow(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        
        res = []
        d = collections.deque()
        
        for i, n in enumerate(nums):
            
            while d and nums[d[-1]] < n: #当前的值为n，如果，队列中的数（-1位置）小于n，则弹出，队列d[0]位置只保存当前窗口的最大值，d中的数为从大到小的排列
                d.pop()
            
            d.append(i)
            if d[0] == i-k:
                d.popleft()  
                
            if i >= k-1: #从此开始，res保存最大值的。
                res.append(nums[d[0]])
                
        return res  
```





https://leetcode-cn.com/problems/sliding-window-maximum/solution/shuang-xiang-dui-lie-jie-jue-hua-dong-chuang-kou-z/




## 题目

Given *n* non-negative integers非负整数 representing an elevation海拔，高度 map where the width of each bar is 1每个柱的宽度为1, compute how much water it is able to trap捕获 after raining.

![img](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)
The above elevation map高度图 is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. **Thanks Marcos** for contributing this image!

**Example:**

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

## 解法

这道题真正**难点**在于: 在一个位置能容下的雨水量等于它左右两边柱子最大高度的最小值减去它的高度.比如下图所示

![Snipaste_2019-05-11_18-02-16.png](https://pic.leetcode-cn.com/6db1fe9019dfbf4d5c2e472112c5cd227925d4b5a99ac48cd2a2779d2535b6ce-Snipaste_2019-05-11_18-02-16.png)

位置`i`能容下雨水量:`min(3,1) - 0 = 1`

所以,问题就变成了: 如何找所有位置的左右两边的柱子的最大值?

这里有3种方法:

思路一:动态规划

思路二:双指针

思路三:栈

时间复杂度都是:*O*(*n*)



思路一: 动态规划

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        if not height: return 0
        
        n = len(height)
        max_left = [0] * n
        max_right = [0] * n
        max_left[0] = height[0]
        max_right[-1] = height[-1]
        # 找位置i左边最大值
        for i in range(1, n):
            max_left[i] = max(height[i], max_left[i-1])
        # 找位置i右边最大值
        for i in range(n-2, -1, -1):
            max_right[i] = max(height[i], max_right[i+1])
        #print(max_left)
        #print(max_right)
        # 求结果
        res = 0
        for i in range(n):
            res += min(max_left[i], max_right[i]) - height[i]
        return res
```





#### 方法 2：动态编程

**直观想法**

在暴力方法中，我们仅仅为了找到最大值每次都要向左和向右扫描一次。但是我们可以提前存储这个值。因此，可以通过动态编程解决。

这个概念可以见下图解释：

![trapping_rain_water.png](https://pic.leetcode-cn.com/53ab7a66023039ed4dce42b709b4997d2ba0089077912d39a0b31d3572a55d0b-trapping_rain_water.png)

**算法**

- 找到数组中从下标 i 到最左端最高的条形块高度 left_max。
- 找到数组中从下标 i 到最右端最高的条形块高度 right_max。
- 扫描数组 height 并更新答案

```c++
int trap(vector<int>& height)
{
	if(height == null)
		return 0;
    int ans = 0;
    int size = height.size();
    vector<int> left_max(size), right_max(size);
    left_max[0] = height[0];
    for (int i = 1; i < size; i++) {
        left_max[i] = max(height[i], left_max[i - 1]);
    }
    right_max[size - 1] = height[size - 1];
    for (int i = size - 2; i >= 0; i--) {
        right_max[i] = max(height[i], right_max[i + 1]);
    }
    for (int i = 1; i < size - 1; i++) {
        ans += min(left_max[i], right_max[i]) - height[i];
    }
    return ans;
}
```










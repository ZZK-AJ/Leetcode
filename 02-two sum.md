题目：

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。 

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9

所以返回 [0, 1] 



Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice. 

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,return [0, 1].



解题思路：

我们应该首先想用暴力求解的话，怎么做？

我们会遍历数组 a，然后看除了 a 数组中有没有 target-a 的数，这样就能保证该数组有两个数和等于 target；但是时间复杂度为 O(n^2) 

其实，我们可以利用空间换时间

用哈希（Python 叫字典）先求出每一个对应值，对应target的值是多少遍历元素的时候，记录元素的下标，当我们找 target-a 时候，只需要在字典找，就可以了，查找字典时间复杂度为 O(1) 所以，时间复杂度：O(n)  空间复杂度：O(n)

```python
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        h_map = {}
        for index, num in enumerate(nums):
            another_num = target - num
            if another_num in h_map:
                return [h_map[another_num], index]
            h_map[num] = index
        return None

input_l = [1,2,3,5,13,6,34]
c = Solution()
c.twoSum(input_l,9)

# inp = {1:22,2:33,3:44}
# print(inp[3])
# 44
```




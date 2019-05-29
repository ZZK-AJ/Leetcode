## 题目

Given an array `nums` of *n* integers, are there elements *a*, *b*, *c* in `nums` such that *a* + *b* + *c* = 0? Find all unique triplets三胞胎 in the array which gives the sum of zero.

**Note:**

The solution set must not contain duplicate triplets.

**Example:**

```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```



## 解法

1. 简单的暴力循环法：

一个新的周末，你再次去现在参加了一个街篮比赛，赛前当然要组队啦，现在要想一个方法找到队友。组队还有一个要求，就是队伍的平均实力要符合要求，比如菜鸟抱两个大腿，或者有王者带两个弱鸡。

我们先想一个保底的办法，再去慢慢优化。最简单的办法是，每个人都去依次拉上另一个人一起去找第三个人，这个时间复杂度是O(n3)。

```javascript
    var threeSum = function(nums) {
      let res = []
      for (let i = 0; i < nums.length - 2; i++) { // 每个人
        for (let j = i + 1; j < nums.length - 1; j++) { // 依次拉上其他每个人
          for (let k = j + 1; k < nums.length; k++) { // 去问剩下的每个人
            if (nums[i] + nums[j] + nums[k] === 0) { // 我们是不是可以一起组队
              res.push([nums[i], nums[j], nums[k]])
            }
          }
        }
      }
      return res
    }
```

受到上题的启发，在凑齐两人以后，他们可以找主持人登记需求的第三人，而不需要在茫茫人海中去找队友。这样，我们就把问题优化成了每个人都要找其他每个人，即时间复杂度O(n2)，因为需要主持人记录数据，这里还有O(n)的空间复杂度。

```
    var threeSum = function(nums) {
        let res = []
        let hash = {}
        for (let i = 0; i < nums.length - 2; i++) { // 每个人
          for (let j = i + 1; j < nums.length - 1; j++) { // 依次拉上其他每个人
            if (hash[nums[j]] !== undefined) { // 已经有合适自己的两人组
              res.push([nums[j]].concat(hash[nums[j]]))
              hash[nums[j]] = undefined
            } else { // 没有合适自己的两人组
              let mark = 0 - nums[i] - nums[j]
              hash[mark] = [nums[i], nums[j]]
            }
          }
        }
        return res
    } // 示意代码 未AC
```







2. 利用set和dict进行去重和记录：

```python
def threeSum(nums):
    if len(nums) < 3:
        return []
    nums.sort()     # 先排序，后面利于去重
    res = set()

    for i,v in enumerate(nums[:-2]):    # 不取到排序后的最后两个？因为当v遍历到倒数第三个的时候，就都遍历完了，是3sum来的
        if i>=1 and v == nums[i-1]:     # v == nums[i-1] 是防止为了去重，
            continue
        d = {}
        for x in nums[i+1:]:        # 这里遍历x，列表剩下的元素
            if x not in d:      # 假如x不在d里面，就是把 -v-x 放入d，然后还是遍历x，看看有没有符合的x
                d[-v-x] = 1
            else:
                res.add((v,-v-x,x))
    return [list(i) for i in res]

nums = [-1, 0, 1, 2, -1, -4]
print(threeSum(nums))
```



3. 节省空间复杂度，利用双指针进行移动

```python
def threeSum2(nums):
    res = []    # 用于存放最后结果
    nums.sort() # 排序，用于去重和后面l和r的移动
    for i in range(len(nums)-2):    # 只需要迭代到倒数第三个就行了
        if i>0 and nums[i] == nums[i-1]:    # 去重，和前面一样的就不用重复计算了
            continue
        l, r = i+1,len(nums)-1  # l为i的下一个，r设为最后一个
        while l<r:      # 当两者没有重叠的时候
            s = nums[i] + nums[l] + nums[r]     # 循环，计算三者的和
            if s<0: l+=1    # 假如小于0，说明需要更大，因为是排好序的，所以l往右移，继续计算
            elif s>0: r-=1      # 小于0，说明需要更小的，所以l往左移，继续计算
            else:
                res.append((nums[i], nums[l], nums[r]))     # 等于0的情况，满足
                """
                # 只是为了减少运算次数，就假如相等的情况，就顺移一位，去掉也可以的?
                不可以去掉！！！因为要用于去重
                讨论这种情况：
                输入  [-2,0,0,2,2]
                输出  [[-2,0,2],[-2,0,2]]
                预期结果    [[-2,0,2]]
                """
                while l<r and nums[l] == nums[l+1]:
                    l += 1
                while l<r and nums[r] == nums[r-1]:
                    r -= 1
                l+=1; r-=1  # 不然还是继续两边往中间移
    return res

nums = [-1, 0, 1, 2, -1, -4]
# print(nums[:-1])
print(threeSum2(nums))
```






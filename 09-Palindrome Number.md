[TOC]

### Problem

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

**Example 1:**

```
Input: 121
Output: true
```

**Example 2:**

```
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

**Example 3:**

```
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

Follow up:

Coud you solve it without converting the integer to a string?

### 使用字符串的解法(python)

直接用字符串反转比较就行了 `[::-1]`

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x < 0:
            return False
        reversed_x = int(str(x)[::-1])
        if reversed_x == x:
            return True
        else:
            return False

a = 12321
# a = 120
# a = -11     # 在输入-11会报错，所以要先判断正负
# a = 2332
c = Solution()
result = c.isPalindrome(a)
print(result)
```

### 不使用str的解法(python)

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        """
        反转整数 如果反转后到一半出现反转后一半与前一半相等(abba型)或者等于前一半整除10则是回文串(aba型)
        121 -> 12,1
        1221 -> 12,21
        :param x:
        :return:
        """
        if (x < 0) or (x != 0 and x % 10 == 0):
            return False
        cmp_num = 0
        print(x)
        print('==='*13)
        while x > cmp_num:
            print(cmp_num*10,x%10)
            cmp_num = cmp_num * 10 + x % 10     # x%10为对x取余,返回余数
            print('cmp_num: ',cmp_num)
            x //= 10
            print('x: ',x)
            print('---'*13)
        #print(x,cmp_num)
        return x == cmp_num or x == cmp_num // 10       # 如123//10=12得到整除的得数

a = 121
# a = 123321
# a = -11     # 在输入-11会报错，所以要先判断正负
# a = 2332
c = Solution()
result = c.isPalindrome(a)
print(result)
```

#### 另外一种直接的思路

```python
# class Solution:
#     def isPalindrome(self, x: int) -> bool:
#        # 定义一个变量存储x的值
#         prev_x = x
#         # 定义一个变量存储x倒序后的值
#         inve_x = 0
#         # 当prev_x大于0的时候循环，这里筛选负数
#         while prev_x > 0:
#             # inve_x*10加上prev_x和10取余的数
#             inve_x = inve_x * 10 + (prev_x % 10)
#             print(inve_x)
#             # prev_x整除10
#             prev_x = prev_x // 10
#             print(prev_x)
#             print('---')
#         return inve_x == x
#
# if __name__ == '__main__':
#     s = Solution()
#     palindrome_bool = s.isPalindrome(121)
#     print(palindrome_bool)

```

### JAVA版解法

```java
// 后续补充

```


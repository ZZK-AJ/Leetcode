解决的代码如下：

```python
class Solution:
    def reverse(self, x: int) -> int:
        flag = -1 if x < 0  else 1
        res = flag * int(str(abs(x))[::-1])
        return res if (-2**31)<=res<=(2**31-1) else 0

a = 121341
c = Solution()
result = c.reverse(a)
print(result)
```


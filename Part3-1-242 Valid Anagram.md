## 题目

Given two strings *s* and *t* , write a function to determine if *t* is an anagram of *s*.

**Example 1:**

```
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2:**

```
Input: s = "rat", t = "car"
Output: false
```

**Note:**
You may assume假设 the string contains only lowercase alphabets.

**Follow up:**
What if the inputs contain unicode characters? How would you adapt your solution to such case?

## 解法

1. 直接利用排序的方法，排序后查看是否完全一样，是O(nlogn)的复杂度

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return sorted(s) == sorted(t)
```

执行用时 : 88 ms, 在Valid Anagram的Python3提交中击败了61.90% 的用户
内存消耗 : 14 MB, 在Valid Anagram的Python3提交中击败了29.92% 的用户



2. 利用map，把对应的存入map，然后进行比较

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        d1,d2 = {},{}
        for i in s:
            d1[i] = d1.get(i,0) + 1
        for i in t:
            d2[i] = d2.get(i,0) + 1
        return d1 == d2
```

这里d1.get(i) 是取字典里面 i 的具体值，后面为什么使用了 d1.get(i,0) ? 因为一开始要给一个默认值 0 

```python
dict.get(key, default=None)
```

执行用时 : 80 ms, 在Valid Anagram的Python3提交中击败了74.18% 的用户

内存消耗 : 13.1 MB, 在Valid Anagram的Python3提交中击败了96.96%的用户



```java
class Solution {
    public boolean isAnagram_1(String s, String t) {
        char[] sChars = s.toCharArray();
        char[] tChars = t.toCharArray();
        Arrays.sort(sChars);
        Arrays.sort(tChars);
        return String.valueOf(sChars).equals(String.valueOf(tChars));
    }

    public boolean isAnagram_2(String s, String t) {
        Map<Character, Integer> map = new HashMap<>();
        for (char ch : s.toCharArray()) {
            map.put(ch, map.getOrDefault(ch, 0) + 1);
        }
        for (char ch : t.toCharArray()) {
            Integer count = map.get(ch);
            if (count == null) {
                return false;
            } else if (count > 1) {
                map.put(ch, count - 1);
            } else {
                map.remove(ch);
            }
        }
        return map.isEmpty();
    }

    public boolean isAnagram(String s, String t) {
        int[] sCounts = new int[26];
        int[] tCounts = new int[26];
        for (char ch : s.toCharArray()) {
            sCounts[ch - 'a']++;
        }
        for (char ch : t.toCharArray()) {
            tCounts[ch - 'a']++;
        }
        for (int i = 0; i < 26; i++) {
            if (sCounts[i] != tCounts[i]) {
                return false;
            }
        }
        return true;
    }
}
```

第一种解法：

执行用时 : 10 ms, 在Valid Anagram的Java提交中击败了54.74% 的用户

内存消耗 : 41.5 MB, 在Valid Anagram的Java提交中击败了34.17% 的用户

第二种：

执行用时 : 50 ms, 在Valid Anagram的Java提交中击败了19.43% 的用户

内存消耗 : 42.1 MB, 在Valid Anagram的Java提交中击败了21.88% 的用户

第三种：

执行用时 : 8 ms, 在Valid Anagram的Java提交中击败了69.75% 的用户
内存消耗 : 38.8 MB, 在Valid Anagram的Java提交中击败了84.99% 的用户




## 题目

Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets括号 must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

**Example 1:**

```
Input: "()"
Output: true
```

**Example 2:**

```
Input: "()[]{}"
Output: true
```

**Example 3:**

```
Input: "(]"
Output: false
```

**Example 4:**

```
Input: "([)]"
Output: false
```

**Example 5:**

```
Input: "{[]}"
Output: true
```

## 思路

想象一下，你正在为你的大学课设编写一个小型编译器，编译器的任务之一（或称子任务）将检测括号是否匹配。

我们本文中看到的算法可用于处理编译器正在编译的程序中的所有括号，并检查是否所有括号都已配对。这将检查给定的括号字符串是否有效，是一个重要的编程问题。

使用栈作为该问题的中间数据结构的算法。利用栈先进后出的本质和括号的匹配本质，把左括号放入栈中。

**算法**

1. 初始化栈 S。
2. 一次处理表达式的每个括号。
3. 如果遇到开括号，我们只需将其推到栈上即可。这意味着我们将稍后处理它，让我们简单地转到前面的 **子表达式**（判断两个括号是否匹配）。
4. 如果我们遇到一个闭括号，那么我们检查栈顶的元素。如果栈顶的元素是一个 `相同类型的` 左括号，那么我们将它从栈中弹出并继续处理。否则，这意味着表达式无效。
5. 如果到最后我们剩下的栈中仍然有元素，那么这意味着表达式无效。

## Python解法

```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []  # 引入一个list的数据结构，用于实现栈的效果
        paren_map = {')':'(',']':'[','}':'{'}  # 把右括号放在key处，用于后续的判断 paren_map[c]
        for c in s:
            if c not in paren_map:  #假如字符串不在map内，说明是左括号，放入栈（list）中
                stack.append(c)
            elif not stack or paren_map[c] != stack.pop():  # 假如栈没有元素 或者 paren_map[c]取到的匹配的左括号 不等于 栈顶元素(因为必须是栈顶才符合左右括号一一对应匹配的情况，否则就返回 Flase)
                return False
        return not stack   # 最后还要判断栈是否还有元素，没有就是返回True，有就是Flase了,说明还有未匹配上的左括号
```



```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        # The stack to keep track of opening brackets.
        stack = []
        # Hash map for keeping track of mappings. This keeps the code very clean.
        # Also makes adding more types of parenthesis easier
        mapping = {")": "(", "}": "{", "]": "["}

        # For every bracket in the expression.
        for char in s:
            # If the character is an closing bracket
            if char in mapping:
                # Pop the topmost element from the stack, if it is non empty
                # Otherwise assign a dummy value of '#' to the top_element variable
                top_element = stack.pop() if stack else '#'
                # The mapping for the opening bracket in our hash and the top
                # element of the stack don't match, return False
                if mapping[char] != top_element:
                    return False
            else:
                # We have an opening bracket, simply push it onto the stack.
                stack.append(char)
        # In the end, if the stack is empty, then we have a valid expression.
        # The stack won't be empty for cases like ((()
        return not stack
```





## Java解法

```java
class Solution {
  // Hash table that takes care of the mappings.
  private HashMap<Character, Character> mappings;
  // Initialize hash map with mappings. This simply makes the code easier to read.
  public Solution() {
    this.mappings = new HashMap<Character, Character>();
    this.mappings.put(')', '(');
    this.mappings.put('}', '{');
    this.mappings.put(']', '[');
  }
  public boolean isValid(String s) {
    // Initialize a stack to be used in the algorithm.
    Stack<Character> stack = new Stack<Character>();
    for (int i = 0; i < s.length(); i++) {
      char c = s.charAt(i);
      // If the current character is a closing bracket.
      if (this.mappings.containsKey(c)) {
        // Get the top element of the stack. If the stack is empty, set a dummy value of '#'
        char topElement = stack.empty() ? '#' : stack.pop();
        // If the mapping for this bracket doesn't match the stack's top element, return false.
        if (topElement != this.mappings.get(c)) {
          return false;
        }
      } else {
        // If it was an opening bracket, push to the stack.
        stack.push(c);
      }
    }
    // If the stack still contains elements, then it is an invalid expression.
    return stack.isEmpty();
  }
}
```


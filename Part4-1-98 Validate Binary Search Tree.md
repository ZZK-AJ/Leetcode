## 题目

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than**the node's key.
- Both the left and right subtrees must also be binary search trees.

 

**Example 1:**

```
    2
   / \
  1   3

Input: [2,1,3]
Output: true
```

**Example 2:**

```
    5
   / \
  1   4
     / \
    3   6

Input: [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```

## 解法

1. 利用二叉排序树的性质，中序遍历（左根右），得到的数组，应该是一个升序的排列
2. 使用一个递归函数，对每棵树进行递归，左子树的最大值应该要小于根，右子树的最小值要大于根

时间复杂度都是On



中序遍历，每个节点都跟前一个节点比较，如果前一个节点比当前节点大的话返回False，否则返回True。

![image-20190530121441568](/Users/zzk/Library/Application Support/typora-user-images/image-20190530121441568.png)

```python

class Solution(object):
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        self.prev = None
        return self.helper(root)
        
    def helper(self, root):
        if root is None:
            return True
        if not self.helper(root.left):
            return False
        if self.prev and self.prev.val >= root.val:
            return False
        self.prev = root
        return self.helper(root.right)
```

执行用时 : 64 ms, 在Validate Binary Search Tree的Python3提交中击败了96.91% 的用户
内存消耗 : 16 MB, 在Validate Binary Search Tree的Python3提交中击败了56.60% 的用户



递归验证 ，大致思路如下：

1. 如果当前节点可用，则将当前节点值与其上、下限进行比较
2. 然后对于左、右子树重复该步骤

需要注意以下几点：

程序初始化时，上、下限分别为对应语言中正无穷和负无穷

python中使用float('-inf')和float('inf')表示

递归过程中需不断更新上、下限，左子节点上限为当前节点值，右子节点下限为当前节点值

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

import sys
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        
        def helper(node, lower, upper):
            if not node:
                return True
            
            if node.val > lower and node.val < upper:
                return helper(node.left, lower, node.val) and helper(node.right, node.val, upper)
            else:
                return False
        
        return helper(root, float('-inf'), float('inf'))
```

执行用时 : 64 ms, 在Validate Binary Search Tree的Python3提交中击败了96.91% 的用户
内存消耗 : 15.5 MB, 在Validate Binary Search Tree的Python3提交中击败了96.56% 的用户


```python
class Node:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None


from collections import deque


class Tree:
    def __init__(self):
        self.root = None

    def add(self, val):
        """
        binary tree add val
        思路：前提条件：传入的序列是按照一棵树的层序遍历，也就是广度优先搜索的方法遍历的。
        初始化一棵树的时候，先判断这个子树有无根节点，没有就肯定先赋值根节点 root，有 root 就把 root 放入一个 list 暂存
        有 root 的情况下循环，判断有无 left 和 right 节点，依次赋值对应节点值，然后下次函数调用
        :param val:
        :return:
        """
        node = Node(val)  # 初始化这个值的节点
        print('=' * 99)
        print(node.val)
        if self.root == None:
            pass
        else:
            print("self.root:{}".format(self.root.val))
        if self.root is None:  # 如果根节点 root 是 None ，赋值为 root
            self.root = node  # 为什么这里不 return，因为处于if...else...中
            # return
        else:
            q = [self.root]  # 有 root 节点，创建一个这样的 list

            while True:
                pop_node = q.pop(0)  # 把根节点拿出来
                print("pop_node is : {}".format(pop_node.val))
                if pop_node.left is None:  # 给 left 和 right 赋值
                    pop_node.left = node
                    print("add left: {}".format(node.val))
                    return
                elif pop_node.right is None:
                    pop_node.right = node
                    print("add right: {}".format(node.val))
                    return
                else:
                    q.append(pop_node.left)
                    print("append left: {}".format(pop_node.left.val))
                    q.append(pop_node.right)
                    print("append right: {}".format(pop_node.right.val))

    def levelOrder(self, root):
        """
        层序遍历：[[3], [9, 20], [None, None, 15, 7]]
        :param root:
        :return:
        """
        if not root: return []

        result = []
        queue = deque()
        queue.append(root)

        # visited = set(root)

        while queue:
            level_size = len(queue)
            current_level = []

            for _ in range(level_size):
                node = queue.popleft()
                current_level.append(node.val)
                if node.left: queue.append(node.left)
                if node.right: queue.append(node.right)

            result.append(current_level)
        return result

    def traverse(self):  # 层次遍历
        if self.root is None:
            return None
        q = [self.root]
        res = [self.root.val]
        while q != []:
            pop_node = q.pop(0)
            if pop_node.left is not None:
                q.append(pop_node.left)
                res.append(pop_node.left.val)

            if pop_node.right is not None:
                q.append(pop_node.right)
                res.append(pop_node.right.val)
        return res

    def preorder(self, root):  # 先序遍历
        if root is None:
            return []
        result = [root.val]
        left_item = self.preorder(root.left)
        right_item = self.preorder(root.right)
        return result + left_item + right_item

    def inorder(self, root):  # 中序序遍历
        if root is None:
            return []
        result = [root.val]
        left_item = self.inorder(root.left)
        right_item = self.inorder(root.right)
        return left_item + result + right_item

    def postorder(self, root):  # 后序遍历
        if root is None:
            return []
        result = [root.val]
        left_item = self.postorder(root.left)
        right_item = self.postorder(root.right)
        return left_item + right_item + result


t = Tree()
l = [3, 9, 20, None, None, 15, 7]
for i in l:
    t.add(i)

cc = t.levelOrder(t.root)
print(cc)
# print('层序遍历:',t.traverse())
# print('先序遍历:',t.preorder(t.root))
# print('中序遍历:',t.inorder(t.root))
# print('后序遍历:',t.postorder(t.root))

```




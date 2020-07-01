# 993. Cousins in Binary Tree

完成时间：2020-07-01

原题地址：https://leetcode.com/problems/cousins-in-binary-tree/

## 题目描述

In a binary tree, the root node is at depth 0, and children of each depth k node are at depth k+1.

Two nodes of a binary tree are cousins if they have the same depth, but have different parents.

We are given the root of a binary tree with unique values, and the values x and y of two different nodes in the tree.

Return true if and only if the nodes corresponding to the values x and y are cousins.

Constraints:
- The number of nodes in the tree will be between 2 and 100.
- Each node has a unique integer value from 1 to 100.

## 我的首个 AC

采用深度优先遍历，解法如下：
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isCousins(self, root, x, y):
        """
        :type root: TreeNode
        :type x: int
        :type y: int
        :rtype: bool
        """
        if root.val == x or root.val == y:
            return False

        current_level = [root.left, root.right]
        x_index = None
        y_index = None
        level = 1
        overhead_total = 1

        while True:
            next_level = []
            next_level_empty = True

            # 广度优先遍历，逐个遍历本层的节点
            for i, node in enumerate(current_level):
                if node is None:
                    # 记录下层的节点
                    next_level.append(None)
                    next_level.append(None)
                    continue

                if node.val == x:
                    # 如果将整棵树视为一个一维数组(从下标1开始存放，为了方便计算父节点)，那么该节点所处的下标为 x_index
                    x_index = overhead_total + i + 1
                    if y_index is not None:
                        break
                elif node.val == y:
                    # 如果将整棵树视为一个一维数组(从下标1开始存放，为了方便计算父节点)，那么该节点所处的下标为 y_index
                    y_index = overhead_total + i + 1
                    if x_index is not None:
                        break

                if node.left is not None or node.right is not None:
                    next_level_empty = False

                next_level.append(node.left)
                next_level.append(node.right)

            if x_index is not None and y_index is not None:
                # 如果在本层找齐了 x 和 y，则判断它们的父节点是否相同
                return x_index / 2 != y_index / 2
            elif x_index is not None or y_index is not None:
                # 如果在本层只找到了 x 或只找到了 y，意味着它们不可能是 cousin
                return False
            else:
                if next_level_empty:
                    return False
                current_level = next_level
                overhead_total += pow(2, level)
                level += 1      
```

## 别人的广度优先遍历解法
```python
class Solution:
    def isCousins(self, root, x, y):
        res = []
        def depth(node, parent, d, x, y):
            if node == None or len(res) ==2:
                return

            if node.val == x or node.val == y:
                res.append((parent, d))

            depth(node.left, node, d + 1, x, y)
            depth(node.right, node, d + 1, x, y)

        depth(root, None, 0, x, y)         

        return res[0][0] !=res[1][0] and res[0][1] == res[1][1]
```

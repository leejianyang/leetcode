# 102 - Binary Tree Level Order Traversal

- 完成时间: 2020-07-03
- 原题地址：https://leetcode.com/problems/binary-tree-level-order-traversal/

## 题目描述
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

## 我的首个 AC
```python
class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if root is None:
            return []

        node_queue = [root]
        result = []

        while len(node_queue):
            current_level_size = len(node_queue)

            current_level = []
            for _ in xrange(current_level_size):
                node = node_queue.pop(0)
                current_level.append(node.val)
                if node.left:
                    node_queue.append(node.left)
                if node.right:
                    node_queue.append(node.right)
            result.append(current_level)

        return result
```

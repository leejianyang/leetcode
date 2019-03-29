# 687. Longest Univalue Path

完成时间：2019-03-29

原题：https://leetcode.com/problems/longest-univalue-path/

## 题目描述

Given a binary tree, find the length of the longest path where each node in the path has the same value. This path may or may not pass through the root.

**Note**: The length of path between two nodes is represented by the number of edges between them.

**Note**: The given binary tree has not more than 10000 nodes. The height of the tree is not more than 1000.

## 我的首个 AC

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def longestUnivaluePath(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if root is None:
            return 0
        
        root_tree_length = self.countLength(root.left, root.val) + self.countLength(root.right, root.val)
        left_tree_length = self.longestUnivaluePath(root.left)
        right_tree_length = self.longestUnivaluePath(root.right)
        
        return max(root_tree_length, left_tree_length, right_tree_length)
    
    def countLength(self, node, value):
        if node is None:
            return 0
        if node.val != value:
            return 0
    
        return 1 + max(self.countLength(node.left, value), self.countLength(node.right, value))
```
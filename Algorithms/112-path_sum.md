# 112. Path Sum
- 完成时间：2020-09-07
- 原题地址：https://leetcode.com/problems/path-sum/

## 题目描述
Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

Note: A leaf is a node with no children.

## example
Given the below binary tree and sum = 22,
```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
```

return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.

## 我的 solution
最基本的深度优先搜索算法
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def hasPathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: bool
        """
        return self.search(root, sum)

    def search(self, node, s):
        if node is None:
            return False

        if node.val == s and node.left is None and node.right is None:
            return True

        return self.search(node.left, s-node.val) or self.search(node.right, s-node.val)
```

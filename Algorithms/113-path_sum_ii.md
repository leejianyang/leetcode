# 113. Path Sum II
- 完成时间：2020-09-09
- 原题地址：https://leetcode.com/problems/path-sum-ii/

## 题目描述
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

Note: A leaf is a node with no children.

## Example
Given the below binary tree and sum = 22,
```
5
/ \
4   8
/   / \
11  13  4
/  \    / \
7    2  5   1
```
Return:
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

## 我的解法
深度优先遍历二叉树
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def pathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: List[List[int]]
        """
        result = []
        self.find(root, sum, [], result)
        return result

    def find(self, node, s, current_path, result):
        if node is None:
            return

        current_path.append(node.val)

        if node.val == s and node.left is None and node.right is None:
            result.append(current_path[:])
        else:
            self.find(node.left, s-node.val, current_path, result)
            self.find(node.right, s-node.val, current_path, result)

        del current_path[-1]
```

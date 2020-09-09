# 129. Sum Root to Leaf Numbers

- 完成时间：2020-09-09
- 原题地址：https://leetcode.com/problems/sum-root-to-leaf-numbers/

## 题目描述

Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path 1->2->3 which represents the number 123.

Find the total sum of all root-to-leaf numbers.

Note: A leaf is a node with no children.

## Example

```
Input: [1,2,3]
    1
   / \
  2   3
Output: 25
Explanation:
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.
```

```
Input: [4,9,0,5,1]
    4
   / \
  9   0
 / \
5   1
Output: 1026
Explanation:
The root-to-leaf path 4->9->5 represents the number 495.
The root-to-leaf path 4->9->1 represents the number 491.
The root-to-leaf path 4->0 represents the number 40.
Therefore, sum = 495 + 491 + 40 = 1026.
```

## 我的解法
深度优先遍历算法
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def sumNumbers(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        return self.dfs(root, 0, [])

    def dfs(self, node, total, current_path):
        if node is None:
            return total

        current_path.append(str(node.val))

        if node.left is None and node.right is None:
            total += int(''.join(current_path))
        else:
            total = self.dfs(node.left, total, current_path)
            total = self.dfs(node.right, total, current_path)

        del current_path[-1]

        return total
```

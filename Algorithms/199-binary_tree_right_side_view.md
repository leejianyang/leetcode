# 199. Binary Tree Right Side View

- 完成时间：2020-09-07
- 原题地址：https://leetcode.com/problems/binary-tree-right-side-view/

## 题目描述

Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

## Example

```
Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```

## 我的 Solution
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def rightSideView(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        next_level = [root]
        result = []
        if not root:
            return []

        while next_level:
            current_level = next_level
            next_level = []
            result.append(current_level[-1].val)
            for node in current_level:
                if node.left:
                    next_level.append(node.left)
                if node.right:
                    next_level.append(node.right)

        return result
```

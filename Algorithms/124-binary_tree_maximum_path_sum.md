# 124. Binary Tree Maximum Path Sum

- 完成时间：2020-09-10
- 原题地址：https://leetcode.com/problems/binary-tree-maximum-path-sum/

## 题目描述

Given a non-empty binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

## Example
```
Input: [1,2,3]

       1
      / \
     2   3

Output: 6
```

```
Input: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

Output: 42
```

## 我的Solution
```python
import sys
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def maxPathSum(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """        
        return self.dfs(root, -sys.maxint-1)[1]

    def dfs(self, node, current_max):
        if node.left is None and node.right is None:
            return node.val, max(current_max, node.val)

        if node.left:
            left_side, current_max = self.dfs(node.left, current_max)
        else:
            left_side = None
        if node.right:
            right_side, current_max = self.dfs(node.right, current_max)
        else:
            right_side = None

        total = node.val
        with_left_side = node.val
        with_right_side = node.val

        if left_side is not None:
            with_left_side += left_side
            total += left_side
        if right_side is not None:
            with_right_side += right_side
            total += right_side

        current_max = max(current_max, node.val, with_left_side, with_right_side, total, left_side, right_side)

        return max(with_left_side, with_right_side, node.val), current_max
```

解法的思路是深度优先遍历。假如有一颗两层的二叉树，父节点为a，左孩子为b，右孩子为c，那么按题目的要求，最大值可能在以下6种情况中出现：
- （1）a
- （2）b
- （3）c
- （4）a+b+c
- （5）a+b
- （6）a+c

在每一层的递归遍历过程中，都将这6种情况中的最大值与之前已知的最大值进行比较，得到当前已知的最大值。然后还要把当层的最大值往上层传递（递归返回)，但是以上的(2)、(3)、(4)是无法向上传递的，所以只能将(1)、(5)、(6)的最大值向上传递 

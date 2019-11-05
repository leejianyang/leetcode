# 230. Kth Smallest Element in a BST

完成时间：2019-11-05

原题地址：https://leetcode.com/problems/kth-smallest-element-in-a-bst/

## 题目描述

Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

Note:
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

## Example

Example 1：
```
Input: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
Output: 1
```
Example 2：
```
Input: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
Output: 3
```

## 我的首个解法
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def kthSmallest(self, root, k):
        """
        :type root: TreeNode
        :type k: int
        :rtype: int
        """
        _, target = self.find(root, k)
        return target
    
    def find(self, root, k):
        left_count = 0
        right_count = 0
        
        if root.left is not None:
            left_count, target = self.find(root.left, k)
            if target is not None:
                return left_count, target
        
        if left_count == k - 1:
            # 找到了目标值
            return left_count, root.val
        
        if root.right is not None:
            right_count, target = self.find(root.right, k-left_count-1)
            if target is not None:
                return right_count, target
        return left_count+right_count+1, None
```
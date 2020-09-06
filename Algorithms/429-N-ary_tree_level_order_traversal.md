# 429. N-ary Tree Level Order Traversal

- 完成时间：2020-09-06
- 原题地址：https://leetcode.com/problems/n-ary-tree-level-order-traversal/

## 题目描述

Given an n-ary tree, return the level order traversal of its nodes' values.

Nary-Tree input serialization is represented in their level order traversal, each group of children is separated by the null value (See examples).

Constraints:
- The height of the n-ary tree is less than or equal to 1000
- The total number of nodes is between [0, 10^4]

## Example

```
Input: root = [1,null,3,2,4,null,5,6]
Output: [[1],[3,2,4],[5,6]]
```

```
Input: root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
Output: [[1],[2,3,4,5],[6,7,8,9,10],[11,12,13],[14]]
```

## 我的Solution
```python
"""
# Definition for a Node.
class Node(object):
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""
class Solution(object):
    def levelOrder(self, root):
        """
        :type root: Node
        :rtype: List[List[int]]
        """
        next_level_nodes = []
        result = []
        current_level_vals = []

        if root is None:
            return []
        else:
            next_level_nodes = root.children
            result.append([root.val])

        while next_level_nodes:
            current_level_nodes = next_level_nodes
            next_level_nodes = []
            current_level_vals = []

            for node in current_level_nodes:
                current_level_vals.append(node.val)
                next_level_nodes.extend(node.children)

            result.append(current_level_vals)

        return result
```

## 更简洁的解法

在评论区里面有一个非常简洁的解法，虽然原理也是一样的
```python
class Solution(object):
    def levelOrder(self, root):
        q, ret = [root], []
        while any(q):
            ret.append([node.val for node in q])
            q = [child for node in q for child in node.children if child]
            
        return ret
```

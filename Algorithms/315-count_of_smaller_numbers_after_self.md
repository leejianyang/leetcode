# 315. Count of Smaller Numbers After Self

完成时间：2019-11-17

原题地址：https://leetcode.com/problems/count-of-smaller-numbers-after-self/

## 题目描述

You are given an integer array nums and you have to return a new counts array. The counts array has the property where `counts[i]` is the number of smaller elements to the right of `nums[i]`.

Example:
```
Input: [5,2,6,1]
Output: [2,1,1,0] 
Explanation:
To the right of 5 there are 2 smaller elements (2 and 1).
To the right of 2 there is only 1 smaller element (1).
To the right of 6 there is 1 smaller element (1).
To the right of 1 there is 0 smaller element.
```

## 我的 Solution
```python
class Node(object):
    def __init__(self, val):
        self.val = val
        self.left_child = None
        self.right_child = None
        self.left_side_count = 0
        self.replication_count = 0


class Solution(object):
    def countSmaller(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        if len(nums) == 0:
            return []
        
        output = []
        output.append(0)
        root = Node(nums[-1])
        i = len(nums) - 2

        while i >= 0:
            self.count = 0
            self.insert_tree_and_count(nums[i], root)
            output.append(self.count)
            i -= 1

        return output[::-1]

    def insert_tree_and_count(self, val, node):
        if node is None:
            return Node(val)
        
        if node.val == val:
            node.replication_count += 1
            self.count += node.left_side_count
            return node

        if val < node.val:
            node.left_side_count += 1
            node.left_child = self.insert_tree_and_count(val, node.left_child)
            return node

        if val > node.val:
            self.count += node.left_side_count + 1 + node.replication_count
            node.right_child = self.insert_tree_and_count(val, node.right_child)
            return node
```

这是一个利用二叉搜索树的解法，从尾到头遍历 input 数组，逐个加入二叉搜索树中，并在每个节点中记录比它小的 number 数量（即每个节点的左子树的节点总数）。但这种解法的效率并不太好。

## 使用 Python 自带的 bisect 库
使用 Python 自带的 bisect 库可以轻轻松松完成这道题，而且效率还相当高 -_-
```python
import bisect

class Solution(object):
    def countSmaller(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        temp = []
        output = []
        for num in nums[::-1]:
            count = bisect.bisect_left(temp, num)
            bisect.insort_left(temp, num)
            output.append(count)
        return output[::-1]
```
关于 bisect 库相关的介绍：https://pymotw.com/3/bisect/index.html
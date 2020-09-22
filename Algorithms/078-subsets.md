# 78. Subsets
- 完成时间：2020-09-22
- 原题地址：https://leetcode.com/problems/subsets/

## 题目描述
Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

## Example
```
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

## 我的 Solution
```python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        output = []
        self.go(output, nums, 0)
        return output

    def go(self, output, nums, index):
        if index >= len(nums):
            output.append([])
            return

        self.go(output, nums, index+1)

        for i in range(len(output)):
            new = output[i][:]
            new.append(nums[index])
            output.append(new)
```
以上是回溯的解法。

还有更直观的解法：
```python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        output = [[]]
        for num in nums:
            n = len(output)
            for i in xrange(n):
                new = output[i][:]
                new.append(num)
                output.append(new)
        return output
```

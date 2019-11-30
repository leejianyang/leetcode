# 46. Permutations

完成时间：2019-11-30

原题地址：https://leetcode.com/problems/permutations/

## 题目描述

Given a collection of distinct integers, return all possible permutations.

## Example
```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

## 我的解法
```python
class Solution(object):
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        return self.do(nums)
    
    def do(self, candidate):
        if len(candidate) == 1:
            return [candidate]
        result = []
        for c in candidate:
            subsquence = candidate[:]
            subsquence.remove(c)
            next_round = self.do(subsquence)
            for item in next_round:
                r = [c]
                r.extend(item)
                result.append(r)
        return result
```
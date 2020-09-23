# 90. Subsets II
- 完成时间：2020-09-23
- 原题地址：https://leetcode.com/problems/subsets-ii/

## 题目描述
Given a collection of integers that might contain duplicates, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

## Example
```
Input: [1,2,2]
Output:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

## 我的Solution
```python
class Solution(object):
    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        output = [[]]
        last_num = None

        for num in nums:
            if num != last_num:
                last_num = num
                last_round_add = 0
                for i in xrange(len(output)):
                    new = output[i][:]
                    new.append(num)
                    output.append(new)
                    last_round_add += 1
            else:
                this_round_add = 0
                for i in xrange(len(output)-last_round_add, len(output)):
                    new = output[i][:]
                    new.append(num)
                    output.append(new)
                    this_round_add += 1
                last_round_add = this_round_add


        return output
```

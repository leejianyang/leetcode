# 268. Missing Number

- 完成时间：2020-09-15
- 原题地址：https://leetcode.com/problems/missing-number/

## 题目描述

Given an array containing *n* distinct numbers taken from `0, 1, 2, ..., n`, find the one that is missing from the array.

**Note**:
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

## Example

```
Input: [3,0,1]
Output: 2
```



```
Input: [9,6,4,2,3,5,7,0,1]
Output: 8
```

## 我的解法

```python
class Solution(object):
    def missingNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        i, n = 0, len(nums)
        while i < n:
            j = nums[i]
            if nums[i] < n and nums[i] != nums[j]:
                nums[i], nums[j] = nums[j], nums[i]  # swap
            else:
                i += 1

        # find the first number missing from its index, that will be our required number
        for i in range(n):
            if nums[i] != i:
                return i

        return n

```


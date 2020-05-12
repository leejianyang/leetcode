# 283. Move Zeros

- 完成时间：2020-05-12
- 原题地址：https://leetcode.com/problems/move-zeroes/

## 题目描述

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note:
1. You must do this in-place without making a copy of the array.
2. Minimize the total number of operations.

## Example
```
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```

## 我的首个 AC
```python
class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        left = 0
        right = len(nums) - 1
        
        while left <= right:
            if nums[left] == 0:
                nums[left], nums[right] = nums[right], nums[left]
                i = left
                while i <= right - 2:
                    nums[i], nums[i+1] = nums[i+1], nums[i]
                    i += 1
                right -= 1
            else:
                left += 1
```

## 更优的解法
以上的解法时间复杂度太高了，可以有时间复杂度为 O(n) 的解法：
```python
class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        i = 0
        latestNoneZeroIndex = 0
        while i < len(nums):
            if nums[i] != 0:
                nums[i], nums[latestNoneZeroIndex] = nums[latestNoneZeroIndex], nums[i]
                latestNoneZeroIndex += 1
            i += 1
```
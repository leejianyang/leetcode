# 179. Largest Number

完成时间：2019-04-06

原题：https://leetcode.com/problems/largest-number/

## 题目描述
Given a list of non negative integers, arrange them such that they form the largest number.

**Note**: The result may be very large, so you need to return a string instead of an integer.

## Example
```
Input: [10,2]
Output: "210"
```

```
Input: [3,30,34,5,9]
Output: "9534330"
```

## 我的首个 AC
利用了**快速排序**算法

```python
class Solution(object):
    def largestNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: str
        """
        self.quickSort(nums, 0, len(nums)-1)
        result = ''
        for item in nums:
            result += str(item)
        if result[0] == '0':
            return '0'
        return result
    
    def quickSort(self, nums, start, end):
        if start >= end:
            return
        
        pivot = self.partition(nums, start, end)
        self.quickSort(nums, start, pivot-1)
        self.quickSort(nums, pivot+1, end)
    
    def partition(self, nums, start, end):
        pivot = nums[end]
        pivot_index = end
        
        current = end - 1
        i = start
        j = end - 1
        
        while i < j:
            if self.compare(nums[current], pivot):
                nums[i], nums[current] = nums[current], nums[i]
                i += 1
            else:
                current -= 1
                j -= 1
        
        if self.compare(pivot, nums[i]):
            nums[i], nums[pivot_index] = nums[pivot_index], nums[i]
            pivot_index = i
        else:
            nums[i+1], nums[pivot_index] = nums[pivot_index], nums[i+1]
            pivot_index = i + 1
        return pivot_index
    
    def compare(self, num1, num2):
        return int(str(num1) + str(num2)) > int(str(num2) + str(num1))
```

# 747. Largest Number At Least Twice of Others

完成时间：2019-03-21

原题：https://leetcode.com/problems/largest-number-at-least-twice-of-others/

## 题目描述

In a given integer array nums, there is always exactly one largest element.

Find whether the largest element in the array is at least twice as much as every other number in the array.

If it is, return the index of the largest element, otherwise return -1.

## Example

Example 1:
```
Input: nums = [3, 6, 1, 0]
Output: 1
Explanation: 6 is the largest integer, and for every other number in the array x,
6 is more than twice as big as x.  The index of value 6 is 1, so we return 1.
```

Example 2:
```
Input: nums = [1, 2, 3, 4]
Output: -1
Explanation: 4 isn't at least as big as twice the value of 3, so we return -1.
```

## 我的首个 AC
```python
class Solution(object):
    def dominantIndex(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        max_value = 0
        max_index = -1
        threshold = 0
        
        for index, num in enumerate(nums):
            if max_index == -1:
                if num >= threshold:
                    max_value = num
                    max_index = index
                else:
                    if num * 2 > threshold:
                        threshold = num * 2
            else:
                if num > max_value:
                    if num >= max_value * 2:
                        threshold = max_value * 2
                        max_value = num
                        max_index = index
                    else:
                        threshold = num * 2
                        max_value = 0
                        max_index = -1
                else:
                    if num * 2 >= threshold:
                        if num * 2 <= max_value:
                            pass
                        else:
                            threshold = max_value * 2
                            max_value = 0
                            max_index = -1
                    else:
                        pass
        
        return max_index
```

## 更优解

一看官方给出的 Solution，发现有简洁得多的解法 -.-!
```python
class Solution(object):
    def dominantIndex(self, nums):
        m = max(nums)
        if all(m >= 2*x for x in nums if x != m):
            return nums.index(m)
        return -1
```
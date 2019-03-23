# 41. First Missing Positive

完成时间：2019-03-23

原题：https://leetcode.com/problems/first-missing-positive/

## 题目描述

Given an unsorted integer array, find the smallest missing positive integer.

Your algorithm should run in O(n) time and uses constant extra space.

## Example

```
Input: [1,2,0]
Output: 3
```

```
Input: [3,4,-1,1]
Output: 2
```

```
Input: [7,8,9,11,12]
Output: 1
```

## 我的首个 AC

```python
class Solution(object):
    def firstMissingPositive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        existing_number = {}
        for num in nums:
            if num > 0:
                existing_number[num] = True
        
        num = 0
        while True:
            num += 1
            if not existing_number.get(num, False):
                return num
```

## 更优解法

我的方案中使用了一个额外的字典存储出现过的正整数，在官方论坛中有人给出了利用**原数组**直接存储出现过的正整数的方案：

```python
def firstMissingPositive(self, nums):
    """
    :type nums: List[int]
    :rtype: int
     Basic idea:
    1. for any array whose length is l, the first missing positive must be in range [1,...,l+1], 
        so we only have to care about those elements in this range and remove the rest.
    2. we can use the array index as the hash to restore the frequency of each number within 
         the range [1,...,l+1] 
    """
    nums.append(0)
    n = len(nums)
    for i in range(len(nums)): #delete those useless elements
        if nums[i]<0 or nums[i]>=n:
            nums[i]=0
    for i in range(len(nums)): #use the index as the hash to record the frequency of each number
        nums[nums[i]%n]+=n
    for i in range(1,len(nums)):
        if nums[i]/n==0:
            return i
    return n
```

Bravo!!
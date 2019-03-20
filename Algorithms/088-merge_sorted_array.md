# 88. Merge Sorted Array

完成时间：2019-03-20

原题：https://leetcode.com/problems/merge-sorted-array/

## 题目描述

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:
- The number of elements initialized in nums1 and nums2 are m and n respectively.
- You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2.

## Example

```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

## 我的首个 AC
``` python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: None Do not return anything, modify nums1 in-place instead.
        """
        nums1[m:] = nums2
        
        for index in xrange(m, m+n):
            i = index
            tmp = nums1[index]
            while i>0:
                i -= 1
                if nums1[i] <= tmp:
                    nums1[i+2:index+1] = nums1[i+1:index]
                    nums1[i+1] = tmp
                    break
            else:
                nums1[i+1:index+1] = nums1[i:index]
                nums1[i] = tmp
```
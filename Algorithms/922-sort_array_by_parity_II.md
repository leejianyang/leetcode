# 922. Sort Array By Parity II

完成时间：2019-04-11

原题地址：https://leetcode.com/problems/sort-array-by-parity-ii/

## 题目描述

Given an array A of non-negative integers, half of the integers in A are odd, and half of the integers are even.

Sort the array so that whenever A[i] is odd, i is odd; and whenever A[i] is even, i is even.

You may return any answer array that satisfies this condition.

Note:
1. ```2 <= A.length <= 20000```
2. `A.length % 2 == 0`
3. `0 <= A[i] <= 1000`

## Example
```
Input: [4,2,5,7]
Output: [4,5,2,7]
Explanation: [4,7,2,5], [2,5,4,7], [2,7,4,5] would also have been accepted.
```

## 我的首个 AC
```python
class Solution(object):
    def sortArrayByParityII(self, A):
        """
        :type A: List[int]
        :rtype: List[int]
        """
        data = [None] * len(A)
        
        odd_index = 1
        even_index = 0
        
        for item in A:
            if item % 2 == 0:
                data[even_index] = item
                even_index += 2
            else:
                data[odd_index] = item
                odd_index += 2
        return data
```
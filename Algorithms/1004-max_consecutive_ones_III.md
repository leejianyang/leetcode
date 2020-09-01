# 1004. Max Consecutive Ones III

- 完成时间：2020-08-01
- 原题地址：https://leetcode.com/problems/max-consecutive-ones-iii/

## 原题描述

Given an array A of 0s and 1s, we may change up to K values from 0 to 1.

Return the length of the longest (contiguous) subarray that contains only 1s.

Note:
- 1 <= A.length <= 20000
- 0 <= K <= A.length
- A[i] is 0 or 1

## Example

```
Input: A = [1,1,1,0,0,0,1,1,1,1,0], K = 2
Output: 6
Explanation:
[1,1,1,0,0,1,1,1,1,1,1]
Bolded numbers were flipped from 0 to 1.  The longest subarray is underlined.
```

```
Input: A = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], K = 3
Output: 10
Explanation:
[0,0,1,1,1,1,1,1,1,1,1,1,0,0,0,1,1,1,1]
Bolded numbers were flipped from 0 to 1.  The longest subarray is underlined.
```

## Solution
```python
class Solution(object):
    def longestOnes(self, A, K):
        """
        :type A: List[int]
        :type K: int
        :rtype: int
        """
        left = 0
        right = 0
        zero_count = 0
        max_length = 0

        while right < len(A):
            if A[right] == 1:
                max_length = max(max_length, right-left+1)
                right += 1
            else:
                zero_count += 1
                if zero_count <= K:
                    max_length = max(max_length, right-left+1)
                    right += 1
                else:
                    right += 1
                    while left < right:
                        if A[left] == 1:
                            left += 1
                        else:
                            left += 1
                            zero_count -= 1
                            if zero_count <= K:
                                break

        return max_length
```

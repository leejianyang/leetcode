# 986. Interval List Intersections

完成时间：2020-05-09
原题地址：https://leetcode.com/problems/interval-list-intersections/

## 题目描述
Given two lists of closed intervals, each list of intervals is pairwise disjoint and in sorted order.

Return the intersection of these two interval lists.

(Formally, a closed interval [a, b] (with a <= b) denotes the set of real numbers x with a <= x <= b.  The intersection of two closed intervals is a set of real numbers that is either empty, or can be represented as a closed interval.  For example, the intersection of [1, 3] and [2, 4] is [2, 3].)

## Example
![](https://assets.leetcode.com/uploads/2019/01/30/interval1.png)

```
Input: A = [[0,2],[5,10],[13,23],[24,25]], B = [[1,5],[8,12],[15,24],[25,26]]
Output: [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
Reminder: The inputs and the desired output are lists of Interval objects, and not arrays or lists.
```

## 我的首个AC
```python
class Solution(object):
    def intervalIntersection(self, A, B):
        a_index = 0
        b_index = 0
        output = []

        while a_index < len(A) and b_index < len(B):
            if A[a_index][1] < B[b_index][0]:
                a_index += 1
            elif A[a_index][0] > B[b_index][1]:
                b_index += 1
            else:
                new_output = [None, None]
                new_output[0] = max(A[a_index][0], B[b_index][0])
                new_output[1] = min(A[a_index][1], B[b_index][1])
                output.append(new_output)

                if A[a_index][1] < B[b_index][1]:
                    a_index += 1
                else:
                    b_index += 1

        return output
```
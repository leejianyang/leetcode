# 56. Merge Intervals
- 完成时间：2020-09-13
- 原题地址：https://leetcode.com/problems/merge-intervals/

## 题目描述

Given a collection of intervals, merge all overlapping intervals.

Constraints:
- intervals[i][0] <= intervals[i][1]

## Example
```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

```
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

## 我的solution
```python
class Solution(object):
    def merge(self, intervals):
        """
        :type intervals: List[List[int]]
        :rtype: List[List[int]]
        """
        if not intervals:
            return []
        intervals.sort(key=lambda lst:lst[0])
        
        result = []
        result.append(intervals[0])
        i = 0
        j = 1
        
        
        while j < len(intervals):
            if result[i][1] < intervals[j][0]:
                result.append(intervals[j])
                i += 1
                j += 1
            else:
                result[i] = [result[i][0], max(result[i][1], intervals[j][1])]
                j += 1
        
        return result
```
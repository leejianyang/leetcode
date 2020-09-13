# 57. Insert Interval

- 完成时间：2020-09-13
- 原题地址：https://leetcode.com/problems/insert-interval/

## 题目描述

Given a set of *non-overlapping* intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

## Example

```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```

```
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```

## 我的 solution

```python
class Solution(object):
    def insert(self, intervals, newInterval):
        """
        :type intervals: List[List[int]]
        :type newInterval: List[int]
        :rtype: List[List[int]]
        """
        if not intervals:
            return [newInterval]
        i = 0
        j = 0
        intervalsWihtNew = []
        # 将 newInterval 插入到 intervals 合适的位置
        for i in xrange(len(intervals)):
            if intervals[i][0] >= newInterval[0]:
                if intervals[i][0] == newInterval[0]:
                    if intervals[i][0] < newInterval[1]:
                        intervalsWihtNew.append(intervals[i])
                        intervalsWihtNew.append(newInterval)
                        break
                    else:
                        intervalsWihtNew.append(newInterval)
                        intervalsWihtNew.append(intervals[i])
                        break
                else:
                    intervalsWihtNew.append(newInterval)
                    intervalsWihtNew.append(intervals[i])
                    break
            else:
                intervalsWihtNew.append(intervals[i])
        else:
            intervalsWihtNew.append(newInterval)
        i += 1
        intervalsWihtNew.extend(intervals[i:])
        # 对 intervalsWihtNew 的重合值进行合并，类似 https://github.com/leejianyang/leetcode/blob/master/Algorithms/056-merge_intervals.md
        result = []
        result.append(intervalsWihtNew[0])
        i = 0
        j = 1
        
        while j < len(intervalsWihtNew):
            if result[i][1] < intervalsWihtNew[j][0]:
                result.append(intervalsWihtNew[j])
                i += 1
                j += 1
            else:
                result[i] = [result[i][0], max(result[i][1], intervalsWihtNew[j][1])]
                j += 1
        
        return result
```


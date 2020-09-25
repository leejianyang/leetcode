# 1011. Capacity To Ship Packages Within D Days
- 完成时间：2020-09-25
- 原题地址：https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/

## 题目描述
A conveyor belt has packages that must be shipped from one port to another within D days.

The i-th package on the conveyor belt has a weight of weights[i].  Each day, we load the ship with packages on the conveyor belt (in the order given by weights). We may not load more weight than the maximum weight capacity of the ship.

Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within D days.

## Example
```
Input: weights = [1,2,3,4,5,6,7,8,9,10], D = 5
Output: 15
Explanation:
A ship capacity of 15 is the minimum to ship all the packages in 5 days like this:
1st day: 1, 2, 3, 4, 5
2nd day: 6, 7
3rd day: 8
4th day: 9
5th day: 10

Note that the cargo must be shipped in the order given, so using a ship of capacity 14 and splitting the packages into parts like (2, 3, 4, 5), (1, 6, 7), (8), (9), (10) is not allowed.
```

```
Input: weights = [3,2,2,4,1,4], D = 3
Output: 6
Explanation:
A ship capacity of 6 is the minimum to ship all the packages in 3 days like this:
1st day: 3, 2
2nd day: 2, 4
3rd day: 1, 4
```

```
Input: weights = [1,2,3,1,1], D = 4
Output: 3
Explanation:
1st day: 1
2nd day: 2
3rd day: 3
4th day: 1, 1
```

## 我的解法
```python
class Solution(object):
    def shipWithinDays(self, weights, D):
        """
        :type weights: List[int]
        :type D: int
        :rtype: int
        """
        left = max(weights)
        right = sum(weights)

        while left < right:
            capacity = (left + right) / 2
            days = 1
            current_load = 0
            for w in weights:
                if (current_load + w) > capacity:
                    days += 1
                    current_load = 0
                current_load += w

            if days > D:
                left = capacity + 1
            else:
                right = capacity
        return left
```

看了下讨论区的高赞帖子得到以上解法。

思路是：要逐步尝试不同的方案。关键是，最终的 capacity 一定位于这个区间：[货物重量的最大值, 全部货物重量的总值]，那么就在这个区间内利用「二分查找」的算法来进行尝试。

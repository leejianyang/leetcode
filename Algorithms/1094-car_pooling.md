# 1094. Car Pooling

完成时间：2019-11-25

原题地址：https://leetcode.com/problems/car-pooling/

## 题目描述

You are driving a vehicle that has capacity empty seats initially available for passengers.  The vehicle only drives east (ie. it cannot turn around and drive west.)

Given a list of trips, trip[i] = [num_passengers, start_location, end_location] contains information about the i-th trip: the number of passengers that must be picked up, and the locations to pick them up and drop them off.  The locations are given as the number of kilometers due east from your vehicle's initial location.

Return true if and only if it is possible to pick up and drop off all passengers for all the given trips. 

限制条件：
1. trips.length <= 1000
2. trips[i].length == 3
3. 1 <= trips[i][0] <= 100
4. 0 <= trips[i][1] < trips[i][2] <= 1000
5. 1 <= capacity <= 100000

## Example
Example 1:
```
Input: trips = [[2,1,5],[3,3,7]], capacity = 4
Output: false
```
Example 2:
```
Input: trips = [[2,1,5],[3,3,7]], capacity = 5
Output: true
```
Example 3:
```
Input: trips = [[2,1,5],[3,5,7]], capacity = 3
Output: true
```
Example 4:
```
Input: trips = [[3,2,7],[3,7,9],[8,3,9]], capacity = 11
Output: true
```

## 我的解法
```
class Solution(object):
    def carPooling(self, trips, capacity):
        """
        :type trips: List[List[int]]
        :type capacity: int
        :rtype: bool
        """
        available_seat = [capacity] * 1001

        for p, start, end in trips:
            for i in xrange(start, end):
                if available_seat[i] - p < 0:
                    return False
                else:
                    available_seat[i] -= p
        return True
```
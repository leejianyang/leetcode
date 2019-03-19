# 70. Climbing Stairs

完成时间：2019-03-19

原题：https://leetcode.com/problems/climbing-stairs/

## 题目描述

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

## Example

Example 1:
```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

Example 2:
```
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

## 我的首个 AC
```python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        record = []
        record.append([0] * (n + 1))
        record[0][0] = 1
        current_round = 0
        ways = 0
        
        while True:
            current_round += 1
            record.append([0] * (n + 1))
            j = 0
            while j < n:
                way_count = record[current_round-1][j]
                
                if record[current_round-1][j]:
                    # climb 1 step
                    if j + 1 == n:
                        ways += way_count
                    elif j + 1 > n:
                        pass
                    else:
                        record[current_round][j+1] = way_count + record[current_round][j+1]
                    # climb 2 steps
                    if j + 2 == n:
                        ways += way_count
                    elif j + 2 > n:
                        pass
                    else:
                        record[current_round][j+2] = way_count + record[current_round][j+2]
                j += 1
            for j in xrange(n):
                if record[current_round][j]:
                    break
            else:
                break
        return ways
            
```
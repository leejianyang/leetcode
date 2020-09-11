# 202. Happy Number

- 完成时间：2020-09-11
- 原题地址：https://leetcode.com/problems/happy-number/

## 题目描述

Write an algorithm to determine if a number n is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Return True if n is a happy number, and False if not.

## Example

```
Input: 19
Output: true
Explanation:
1^2 + 9^2 = 82
8^2 + 2^2 = 68
6^2 + 8^2 = 100
1^2 + 0^2 + 0^2 = 1
```

## 我的解法
```python
class Solution(object):
    def isHappy(self, n):
        """
        :type n: int
        :rtype: bool
        """
        slow_pointer = self.get_sum(n)
        faster_pointer = self.get_sum(self.get_sum(n))

        while slow_pointer != 1:
            if slow_pointer == faster_pointer:
                return False

            slow_pointer = self.get_sum(slow_pointer)
            faster_pointer = self.get_sum(self.get_sum(faster_pointer))

        return True


    def get_sum(self, digit):
        result = 0
        for d in str(digit):
            result += int(d) * int(d)
        return result
```

这题的解法与思路与[《141 - Linked List Cycle》](https://github.com/leejianyang/leetcode/blob/master/Algorithms/141-linked_list_cycle.md)思路是一模一样的。将每一步得出的新值串成一个链表，如果这个链表内部存在环，那么意味着该数字不是 happy number，可以停止计算；若链表末尾的值为1，则意味着这个数字是 happy number。

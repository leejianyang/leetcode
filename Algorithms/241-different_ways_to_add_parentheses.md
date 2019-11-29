# 241. Different Ways to Add Parentheses

完成时间：2019-11-29

原题地址：https://leetcode.com/problems/different-ways-to-add-parentheses/

## 题目描述

Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are +, - and *.

## Example
Example 1:
```
Input: "2-1-1"
Output: [0, 2]
Explanation: 
((2-1)-1) = 0 
(2-(1-1)) = 2
```
Example 2:
```
Input: "2*3-4*5"
Output: [-34, -14, -10, -10, 10]
Explanation: 
(2*(3-(4*5))) = -34 
((2*3)-(4*5)) = -14 
((2*(3-4))*5) = -10 
(2*((3-4)*5)) = -10 
(((2*3)-4)*5) = 10
```

## 我的解法
```python
import re

class Solution(object):
    def diffWaysToCompute(self, input):
        """
        :type input: str
        :rtype: List[int]
        """
        numbers, operators = self.split_expression(input)
        result = self.calculator(numbers, operators)
        return result
        
    def split_expression(self, input):
        pattern = re.compile(r'\d+')
        numbers = pattern.findall(input)
        pattern = re.compile(r'[\+\-\*]')
        operators = pattern.findall(input)

        return [numbers, operators]

    def calculator(self, numbers, operators):
        if len(numbers) == 1:
            return numbers

        result = []
        for separated_index in xrange(1, len(numbers)):
            left_part_numbers = numbers[0:separated_index]
            right_part_numbers = numbers[separated_index:]

            operator_separated_index = separated_index - 1
            left_part_operators = operators[0:operator_separated_index]
            right_part_operators = operators[operator_separated_index+1:]
            
            left_part_result = self.calculator(left_part_numbers, left_part_operators)
            right_part_result = self.calculator(right_part_numbers, right_part_operators)

            operator = operators[operator_separated_index]
            for i in left_part_result:
                for j in right_part_result:
                    result.append(eval(str(i) + operator + str(j)))

        return result
```

## 更优雅的解法
在评论区里面看到一个更优雅的解法 >.<
```python
def diffWaysToCompute(self, input):
    if input.isdigit():
        return [int(input)]
    res = []
    for i in xrange(len(input)):
        if input[i] in "-+*":
            res1 = self.diffWaysToCompute(input[:i])
            res2 = self.diffWaysToCompute(input[i+1:])
            for j in res1:
                for k in res2:
                    res.append(self.helper(j, k, input[i]))
    return res
    
def helper(self, m, n, op):
    if op == "+":
        return m+n
    elif op == "-":
        return m-n
    else:
        return m*n
```
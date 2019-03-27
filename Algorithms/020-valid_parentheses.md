# 20. Valid Parentheses

完成时间：2019-03-27

原题：https://leetcode.com/problems/valid-parentheses/

## 题目描述

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:
- Open brackets must be closed by the same type of brackets.
- Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

## Example

```
Input: "()"
Output: true
```

```
Input: "()[]{}"
Output: true
```

```
Input: "(]"
Output: false
```

## 我的首个 AC
```python
class Stack(object):
   
    def __init__(self):
        self._stack = []
        self.index = -1

    def pop(self):
        if self.index < 0:
            return None
        self.index -= 1
        return self._stack.pop()

    def push(self, val):
        self._stack.append(val)
        self.index += 1
    
    def is_empty(self):
        return self.index < 0

class Solution(object):
    
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = Stack()
        
        for item in s:
            if item == '(' or item == '{' or item == '[':
                stack.push(item)
            else:
                top = stack.pop()
                if item == ')':
                    if top != '(':
                        return False
                if item == '}':
                    if top != '{':
                        return False
                if item == ']':
                    if top != '[':
                        return False
        
        if stack.is_empty():
            return True
        return False
```
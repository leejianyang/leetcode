# 17. Letter Combinations of a Phone Number

完成时间：2019-03-18

原题：https://leetcode.com/problems/letter-combinations-of-a-phone-number/

## 题目描述
Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![示例图片](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

## Example

```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

## 我的第一次 AC
```python
import copy

class Solution(object):
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        result = []
        for digit in digits:
            tmp = copy.copy(result)
            result = []
            if tmp:
                for i in xrange(len(tmp)):
                    for s in self.generateString(int(digit), tmp[i]):
                        result.append(s)
            else:
                for s in self.generateString(int(digit), ''):
                    result.append(s)
        return result
            
    
    def getLetterByDigit(self, digit):
        if digit not in (7, 8, 9):
            ascii = 97 + (digit - 2) * 3
            for i in xrange(3):
                yield chr(ascii+i)
        else:
            if digit == 7:
                letter = ['p', 'q', 'r', 's']
            elif digit == 8:
                letter = ['t', 'u', 'v']
            elif digit == 9:
                letter = ['w', 'x', 'y', 'z']
            for l in letter:
                yield l
                
    
    def generateString(self, current_digit, prefix):
        for letter in self.getLetterByDigit(current_digit):
            yield prefix + letter
```

## 别人给出来的更优解法
```python
class Solution(object):
    def letterCombinations(self, digits):
        '''
        :type digits: str
        :rtype: List[str]
        '''
        phone = {'2': ['a', 'b', 'c'],
                 '3': ['d', 'e', 'f'],
                 '4': ['g', 'h', 'i'],
                 '5': ['j', 'k', 'l'],
                 '6': ['m', 'n', 'o'],
                 '7': ['p', 'q', 'r', 's'],
                 '8': ['t', 'u', 'v'],
                 '9': ['w', 'x', 'y', 'z']}    
        result = []
        
        def helpCombine(current, leftoverDigits):
            if not leftoverDigits:
                result.append(current)
                return 
            else:
                for char in phone[leftoverDigits[0]]:
                    helpCombine(current + char, leftoverDigits[1:])
        
        if not digits:
            return []
        else: 
            helpCombine("", digits)
            return result
```
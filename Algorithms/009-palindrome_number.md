# 9. Palindrome Number

完成时间：2019-03-07

原题目：https://leetcode.com/problems/palindrome-number/

## 题目描述

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

## Example

Example 1:
```
Input: 121
Output: true
```

Example 2:
```
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

Example 3:
```
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

## 我的首个 accept
```python
class Solution(object):
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        x = str(x)
        i = 0
        j = len(x) - 1
        is_palindrome = True
        while (i < j):
            if (x[i] == x[j]):
                is_palindrome = True
            else:
                return False
            i += 1
            j -= 1
        return is_palindrome
```

## 进阶要求
Coud you solve it without converting the integer to a string?

我认为以上的代码逻辑简单，在 x 不是特别长的情况下，将 x 转换成字符串两方向扫描的方式已够用。

官方给出的 Solution，不把数字转换成字符串的方式，是要将数字的后半截取出来，进行翻转，然后与前半段比较。
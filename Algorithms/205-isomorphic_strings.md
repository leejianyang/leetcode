# 205. Isomorphic Strings

完成时间：2020-08-21

原题目：https://leetcode.com/problems/isomorphic-strings/

## 题目描述

Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

Note:
You may assume both s and t have the same length.

## example

Example 1:
```
Input: s = "egg", t = "add"
Output: true
```

Example 2:
```
Input: s = "foo", t = "bar"
Output: false
```

Example 3:
```
Input: s = "paper", t = "title"
Output: true
```

## Solution
```python
class Solution(object):
    def isIsomorphic(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        letter_map = {}
        t_appeared = set()

        for i in range(len(s)):
            if s[i] not in letter_map:
                if t[i] in t_appeared:
                    return False
                else:
                    letter_map[s[i]] = t[i]
                    t_appeared.add(t[i])
            else:
                if letter_map[s[i]] != t[i]:
                    return False
        return True
```

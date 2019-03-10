# 14. Longest Common Prefix

完成时间：2019-03-10

原题：https://leetcode.com/problems/longest-common-prefix/

## 题目描述

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

All given inputs are in lowercase letters a-z.

## 例子

Example 1:
```
Input: ["flower","flow","flight"]
Output: "fl"
```

Example 2:
```
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

## 我的首个 AC
```python
class Solution(object):
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        if len(strs) == 0:
            return ""
        if len(strs) == 1:
            return strs[0]
        
        common_prefix = strs[0]
        prefix_len = len(strs[0])
        
        for str in strs[1:]:
            current_len = 0
            for letter in str[0:prefix_len]:
                if letter == common_prefix[current_len]:
                    current_len += 1
                else:
                    break
            if current_len == 0:
                return ''
            else:
                prefix_len = current_len
        return common_prefix[0:prefix_len]
```
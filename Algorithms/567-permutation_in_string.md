# 567. Permutation in String

- 完成时间：2020-09-02
- 原题地址：https://leetcode.com/problems/permutation-in-string/

## 题目描述

Given two strings s1 and s2, write a function to return true if s2 contains the permutation of s1. In other words, one of the first string's permutations is the substring of the second string.

Constraints:

- The input strings only contain lower case letters.
- The length of both given strings is in range [1, 10,000].

## Example
```
Input: s1 = "ab" s2 = "eidbaooo"
Output: True
Explanation: s2 contains one permutation of s1 ("ba").
```

```
Input:s1= "ab" s2 = "eidboaoo"
Output: False
```

## 我的解法
```python
class Solution(object):
    def checkInclusion(self, s1, s2):
        """
        :type s1: str
        :type s2: str
        :rtype: bool
        """
        letter_count = {}
        for i in range(len(s1)):
            letter_count.setdefault(s1[i], 0)
            letter_count[s1[i]] += 1

        left = 0
        right = 0
        match_length = 0

        while right < len(s2):
            right_letter = s2[right]
            if right_letter in letter_count:
                if letter_count[right_letter] > 0:
                    letter_count[right_letter] -= 1
                    match_length += 1
                    right += 1
                    if match_length == len(s1):
                        return True
                elif right_letter == s2[left]:
                    left += 1
                    right += 1
                else:
                    while left < right:
                        letter_count[s2[left]] += 1
                        match_length -= 1
                        if s2[left] == right_letter:
                            left += 1
                            break
                        else:
                            left += 1
                    letter_count[right_letter] -= 1
                    match_length += 1
                    right += 1
            else:
                while left < right:
                    letter_count[s2[left]] += 1
                    left += 1
                    match_length -= 1
                left += 1
                right += 1

        return False
```

这题可以使用滑动窗口算法来解。先统计 s1 字符串中各个单词出现的频次，记在字典 letter_count 中。然后在 s2 字符串中进行窗口滑动，保持当前窗口中每个字母出现的频次，少于或等于 s1 中各个字母分别出现的频次，如果窗口的大小等于 s1 的长度，意味着符合题目条件的子串已经找到了。如果窗口的大小小于 s1 的长度，则继续继续向右扩大窗口。在向右扩大窗口的过程中，一旦打破了「当前窗口中每个字母出现的频次，少于或等于 s1 中各个字母分别出现的频次」这个条件，则窗口的左端要收缩；如果向右扩大窗口的过程中，遇上了 s1 中不存在的字符，那么窗口需要进行重置。

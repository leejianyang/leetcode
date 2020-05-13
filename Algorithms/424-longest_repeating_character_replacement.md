# 424. Longest Repeating Character Replacement

- 完成时间：2020-05-13
- 原题地址：https://leetcode.com/problems/longest-repeating-character-replacement/

## 题目描述

Given a string s that consists of only uppercase English letters, you can perform at most k operations on that string.

In one operation, you can choose any character of the string and change it to any other uppercase English character.

Find the length of the longest sub-string containing all repeating letters you can get after performing the above operations.

**Note**:
Both the string's length and k will not exceed 10^4.

## Example
Example 1:
```
Input:
s = "ABAB", k = 2

Output:
4

Explanation:
Replace the two 'A's with two 'B's or vice versa.
```

Example 2:
```
Input:
s = "AABABBA", k = 1

Output:
4

Explanation:
Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.
```

## 我的首个 AC
```python
class Solution(object):
    def characterReplacement(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: int
        """
        # 当前滑动窗口内各个字母的出现频次
        letter_frequency = {}
        # 滑动窗口的左右端点
        left = 0
        right = 0
        # 当前找到的最长子串
        max_length = 0

        while right < len(s):
            # 将窗口的最新滑入的字母纳入频次统计
            letter_frequency.setdefault(s[right], 0)
            letter_frequency[s[right]] += 1

						# 找出窗口内出现次数最多的字母的频次
            max_letter_count = 0
            for letter, v in letter_frequency.iteritems():
                max_letter_count = max(max_letter_count, v)

						# 当前窗口内，除了出现频次最多的字母外，把其余的字母进行替换后，是否符合要求
            if ((right - left + 1) - max_letter_count) > k:
            		# 若不符合要求，窗口在左侧收缩
                letter_frequency[s[left]] -= 1
                left += 1
            else:
            		# 若符合要求，看看当前窗口的是否目前找到的最长子串
                max_length = max(max_length, right - left + 1)
						
						# 窗口向右扩大
            right += 1

        return max_length
```
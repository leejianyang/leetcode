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

## 进一步优化

以上解法中，每次向右扩大窗口后，都要遍历一次 letter_frequency 来找出当前窗口频率最高的字符，这样是毫无必要的。所以优化了一下代码，效率就可以大幅提升。
```python
class Solution(object):
    def characterReplacement(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: int
        """
        letter_frequency = {}
        left = 0
        right = 0
        max_length = 0

        # 当前窗口内出现最多的字母的频次
        max_letter_count = 0
        # 当前窗口内出现频次最多的字母
        max_letter = None
            
        while right < len(s):
            letter_frequency.setdefault(s[right], 0)
            letter_frequency[s[right]] += 1

            if max_letter is None:
                max_letter_count = 1
                max_letter = s[right]
            else:
                if s[right] == max_letter:
                    max_letter_count += 1
                elif letter_frequency[s[right]] > max_letter_count:
                    # 替换当前窗口内出现最多的字母及其频次
                    max_letter = s[right]
                    max_letter_count = letter_frequency[s[right]]

            if ((right-left+1) - max_letter_count) > k:
                letter_frequency[s[left]] -= 1
                if s[left] == max_letter:
                    max_letter_count -= 1
                left += 1
            else:
                max_length = max(max_length, right-left+1)
            
            right += 1

        return max_length
```
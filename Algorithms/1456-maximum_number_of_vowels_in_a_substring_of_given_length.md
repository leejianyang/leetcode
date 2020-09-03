# 1456. Maximum Number of Vowels in a Substring of Given Length

- 完成时间：2020-09-03
- 原题地址：https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length/

## 题目描述

Given a string s and an integer k.

Return the maximum number of vowel letters in any substring of s with length k.

Vowel letters in English are (a, e, i, o, u).

Constraints:

- 1 <= s.length <= 10^5
- s consists of lowercase English letters.
- 1 <= k <= s.length

## Example

```
Input: s = "abciiidef", k = 3
Output: 3
Explanation: The substring "iii" contains 3 vowel letters.
```

```
Input: s = "aeiou", k = 2
Output: 2
Explanation: Any substring of length 2 contains 2 vowels.
```

```
Input: s = "leetcode", k = 3
Output: 2
Explanation: "lee", "eet" and "ode" contain 2 vowels.
```

```
Input: s = "rhythms", k = 4
Output: 0
Explanation: We can see that s doesn't have any vowel letters.
```

```
Input: s = "tryhard", k = 4
Output: 1
```

## 我的解法
```python
class Solution(object):
    def maxVowels(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: int
        """
        vowel_set = set(['a', 'e', 'i', 'o', 'u'])
        current_count = 0
        max_count = 0
        for i in xrange(k):
            if s[i] in vowel_set:
                current_count += 1
        max_count = current_count

        left = 0
        right = k

        while right < len(s):
            if s[left] in vowel_set:
                current_count -= 1
            left += 1
            if s[right] in vowel_set:
                current_count += 1
            right += 1
            max_count = max(max_count, current_count)

        return max_count
```

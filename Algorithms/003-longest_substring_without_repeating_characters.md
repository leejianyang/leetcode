# 3. Longest Substring Without Repeating Characters

完成时间：2019-03-09

原题：https://leetcode.com/problems/longest-substring-without-repeating-characters/

## 题目描述

Given a string, find the length of the longest substring without repeating characters.

## Example

Example 1:
> Input: "abcabcbb"
> Output: 3 
> Explanation: The answer is "abc", with the length of 3. 

Example 2:
> Input: "bbbbb"
> Output: 1
> Explanation: The answer is "b", with the length of 1.

Example 3:
> Input: "pwwkew"
> Output: 3
> Explanation: The answer is "wke", with the length of 3. 
>             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

## 我的首个 AC
```pyhon
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        max_length = 0
        
        for index, letter in enumerate(s):
            letter_set = set()
            letter_set.add(letter)
            current_length = 1
            for sub_letter in s[index+1:]:
                if sub_letter not in letter_set:
                    letter_set.add(sub_letter)
                    current_length += 1
                else:
                    break
            if current_length > max_length:
                max_length = current_length
        
        return max_length
```

## 改进方案

主要是上面的解法，内层循环每次都要从 index+1 开始遍历，比较耗时。

```php
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function lengthOfLongestSubstring($s) {
        if ($s == '') {
            // 因为 str_split("") 会得到长度为1，有一个空字符串元素的数组
            return 0;
        }
        $maxLength = 0;
        $letterIndex = [];
        $s = str_split($s);
        $startIndex = 0;
        
        foreach ($s as $index => $letter) {
            if (array_key_exists($letter, $letterIndex)) {
                $lastIndex = $letterIndex[$letter];
                if ($lastIndex >= $startIndex) {
                    $startIndex = $lastIndex + 1;
                }
            }
            $letterIndex[$letter] = $index;
            $currentLength = $index - $startIndex + 1;
            $maxLength = max($currentLength, $maxLength);
        } 
        return $maxLength;
    }
}
```
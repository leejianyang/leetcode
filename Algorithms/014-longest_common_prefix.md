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

## 别的解法

看了官方给出来的 Solution 之后，发现有别的几种解法。

### 垂直扫描

像我的首个 AC 那样的算法，逐个逐个字符串来找最长子串，属于「横向扫描」；也可以改成「垂直扫描」，即从下标 0 开始，每个字符串都先判断下标 0 是否相同，接着判断每个字符串的下标 1，如此类推。

这种方案的 worst case 时间复杂度跟横向扫描差不多，不过某些情况下比横向扫描更高效。

```php
class Solution {

    /**
     * @param String[] $strs
     * @return String
     */
    function longestCommonPrefix($strs) {
        if (empty($strs)) {
            return '';
        }
        
        for ($i = 0; $i < strlen($strs[0]); $i++) {
            for ($j = 1; $j < count($strs); $j++) {
                if ($strs[$j][$i] !== $strs[0][$i]) {
                    return substr($strs[0], 0, $i);
                }
            }    
        }
        
        return substr($strs[0], 0, $i);
    }
}
```

### 分治法

```python
class Solution(object):
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        size = len(strs)
        
        if size == 0:
            return ''
        if size == 1:
            return strs[0]
        
        return self.divide(strs, 0, size-1)
        
    
    def divide(self, strs, i, j):
        if i == j:
            return strs[i]
        
        mid = (i + j) / 2
        left_prefix = self.divide(strs, i, mid)
        right_prefix = self.divide(strs, mid+1, j)
        return self.compairTwoString(left_prefix, right_prefix)
    
    def compairTwoString(self, str1, str2):
        length = min(len(str1), len(str2))
        for i in xrange(length):
            print str1[i], str2[i]
            if str1[i] != str2[i]:
                return str1[0:i]
        return str1[0:length]
```
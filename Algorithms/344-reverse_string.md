# 344. Reverse String

- 原题地址：https://leetcode.com/problems/reverse-string/
- 完成时间：2021-02-20

## 题目描述

Write a function that reverses a string. The input string is given as an array of characters char[].

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

You may assume all the characters consist of printable ascii characters.

## Example
```
Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

```
Input: ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```

## 我的解法
```go
func reverseString(s []byte)  {
    i := 0
    j := len(s) - 1
    for i < j {
        s[i], s[j] = s[j], s[i]
        i++
        j--
    }
}
```

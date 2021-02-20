# 387. First Unique Character in a String

- 完成时间：2021-02-20
- 原题地址：https://leetcode.com/problems/first-unique-character-in-a-string/

## 题目描述

Given a string, find the first non-repeating character in it and return its index. If it doesn't exist, return -1.

## Example

```
s = "leetcode"
return 0.

s = "loveleetcode"
return 2.
```

## 我的解法
```go
func firstUniqChar(s string) int {
    m := make(map[rune]int)

    for _, v := range(s) {
        m[v] += 1       
    }

    for i, v := range(s) {
        if m[v] == 1 {
            return i
        }
    }
    return -1
}
```

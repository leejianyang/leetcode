# 350. Intersection of Two Arrays II

- 完成时间：2021-02-05
- 原题地址：https://leetcode.com/problems/intersection-of-two-arrays-ii/

## 题目描述

Given two arrays, write a function to compute their intersection.

Note:
- Each element in the result should appear as many times as it shows in both arrays.
- The result can be in any order.

## Example

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```

```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
```

## Solution
```go
func intersect(nums1 []int, nums2 []int) []int {
    m := make(map[int]int)
    var result []int

    for _, v := range nums1 {
        if _, ok := m[v]; ok {
            m[v] += 1
        } else {
            m[v] = 1
        }
    }

    for _, v := range nums2 {
        if _, ok := m[v]; ok {
            if m[v] > 0 {
                m[v] -= 1
                result = append(result, v)
            }
        }
    }

    return result
}
```

如果 nums1 和 nums2 是有序的话，可以将算法改成这样：
```go
func intersect(nums1 []int, nums2 []int) []int {
    sort.Ints(nums1)
    sort.Ints(nums2)

    var result []int

    i := 0
    j := 0

    for i < len(nums1) && j < len(nums2) {
        if nums1[i] == nums2[j] {
            result = append(result, nums1[i])
            i++;
            j++;
        } else if nums1[i] < nums2[j] {
            i++;
        } else {
            j++;
        }
    }

    return result
}
```

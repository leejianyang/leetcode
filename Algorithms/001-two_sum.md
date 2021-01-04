# 1. Two Sum

完成时间：2019-03-06

原题目：https://leetcode.com/problems/two-sum/

## 问题描述

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

## Example

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## 我的首个 accept

```Python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        input_dict = {}
        for index, item in enumerate(nums):
            if input_dict.get(item) is not None:
                input_dict[item] = [input_dict[item], index]
            else:
                input_dict[item] = index

        for index, item in enumerate(nums):
            another_one = target - item
            if (another_one == item):
                if isinstance(input_dict[item], list):
                    return input_dict[item]
                continue
            another_one_index = input_dict.get(another_one)
            if another_one_index is None:
                continue
            else:
                return [index, another_one_index]
```
## 可优化之处
- 遍历了两次 nums
- 对于 nums 中有两个元素的值相同的情况，处理得过于复杂

## 官方给出的 Solution

### Two-pass Hash Table

可以借鉴的地方是，input_dict 字典直接存 item 在 nums 中第二次出现的下标；当二次遍历 nums 时，若 item 存在于 input_dict，但值不等于当前下标，则证明 nums 中有另一个相同的数字存在，并能马上返回结果

### One-pass Hash Table

直接进行第二次 nums 遍历，若当前遍历的下标是 0，元素是 3，target 是 10，则直接设 input_dict[7] = 0

## 优化后的解法

```
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        complement_dict = {}

        for index, num in enumerate(nums):
            complement = target - num
            if (complement_dict.get(complement) is not None):
                return [complement_dict.get(complement), index]
            else:
                complement_dict[num] = index
```

## Go语言版本
```go
func twoSum(nums []int, target int) []int {
    m := make(map[int]int)

    for i := 0; i < len(nums); i++ {
        if _, ok := m[target-nums[i]]; ok {
            return []int{i, m[target-nums[i]]}
        }
        m[nums[i]] = i
    }

    return []int{}
}
```

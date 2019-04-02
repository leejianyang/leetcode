# 75. Sort Colors

完成时间：2019-04-02
原题：https://leetcode.com/problems/sort-colors/

## 题目描述

Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note: You are not suppose to use the library's sort function for this problem.

## Example

```
Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```

## 我的首个 AC
```python
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        red = 0
        white = 0
        blue = 0
        
        for item in nums:
            if item == 0:
                red += 1
            elif item == 1:
                white += 1
            else:
                blue += 1
        
        for x in xrange(red):
            nums[x] = 0
        
        for x in xrange(white):
            nums[x+red] = 1
        
        for x in xrange(blue):
            nums[x+red+white] = 2
```

## 用排序算法来解

首个 AC 是一个比较取巧的算法，时间复杂度是 O(n)，但需要额外的存储空间。为了练练手，用两种时间复杂度为 O(n^2) 的算法来解。

### 插入排序的解法
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return NULL
     */
    function sortColors(&$nums) {
        $length = count($nums);
        
        for ($i = 1; $i < $length; ++$i) {
            $tmp = $nums[$i];
            
            for ($j = $i-1; $j >= 0; --$j) {
                if ($tmp >= $nums[$j]) {
                    break;
                } else {
                    $nums[$j+1] = $nums[$j];
                }
            }
            $nums[$j+1] = $tmp;
        }
    }
}
```

### 选择排序的解法
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return NULL
     */
    function sortColors(&$nums) {
        $length = count($nums);
        
        for ($i = 0; $i < $length-1; $i++) {
            $minimumIndex = $i;
            for ($j = $i; $j < $length; $j++) {
                if ($nums[$j] < $nums[$minimumIndex]) {
                    $minimumIndex = $j;
                }
            }
            
            $tmp = $nums[$minimumIndex];
            $nums[$minimumIndex] = $nums[$i];
            $nums[$i] = $tmp;
        }
    }
}
```
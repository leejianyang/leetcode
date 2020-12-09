# 739. Daily Temperatures

- 完成时间：2020-12-09
- 原题地址：https://leetcode.com/problems/daily-temperatures/

## 题目描述

Given a list of daily temperatures T, return a list such that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead.

For example, given the list of temperatures `T = [73, 74, 75, 71, 69, 72, 76, 73]`, your output should be `[1, 1, 4, 2, 1, 1, 0, 0]`.

Note: The length of temperatures will be in the range `[1, 30000]`. Each temperature will be an integer in the range `[30, 100]`.

## 我的解法

```php
class Solution {

    /**
     * @param Integer[] $T
     * @return Integer[]
     */
    function dailyTemperatures($T) {
        $stack = [];
        $output = [];

        for ($i = 0; $i < count($T); $i++) {
            $output[] = 0;
        }

        foreach ($T as $index => $t) {
            while ($stack && $t > $T[$stack[count($stack)-1]]) {
                $top = array_pop($stack);
                $output[$top] = $index - $top;
            }
            $stack[] = $index;
        }

        return $output;
    }
}
```

利用一个栈结构记录已遍历过 T 数组中未找到比它的大的元素的下标，注意这个栈是单调递减的（栈底的元素最大，栈顶的元素最小）。

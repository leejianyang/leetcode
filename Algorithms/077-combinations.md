# 77. Combinations

- 完成时间：2020-12-14
- 原题地址：https://leetcode.com/problems/combinations/

## 题目描述

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

You may return the answer in any order.

Constraints:
- 1 <= n <= 20
- 1 <= k <= n

## Example

```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

```
Input: n = 1, k = 1
Output: [[1]]
```

## 我的解法
```php
class Solution {

    /**
     * @param Integer $n
     * @param Integer $k
     * @return Integer[][]
     */
    function combine($n, $k) {
        $output = [];

        $dfs = function ($result, $digit) use (&$output, &$dfs, $k, $n) {
            for ($d = $digit; $d <= $n; $d++) {
                $tmp = $result;
                $tmp[] = $d;
                if (count($tmp) == $k) {
                    $output[] = $tmp;
                } else {
                    $dfs($tmp, $d+1);
                }
            }
        };

        $dfs([], 1);

        return $output;
    }
}
```

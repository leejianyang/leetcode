# 110. Balanced Binary Tree

- 完成时间: 2020-12-18
- 原题地址：https://leetcode.com/problems/balanced-binary-tree/

## 题目描述

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:
> a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

## Example
```
Input: root = [3,9,20,null,null,15,7]
Output: true
```

```
Input: root = [1,2,2,3,3,null,null,4,4]
Output: false
```

```
Input: root = []
Output: true
```

## 我的解法
使用递归求解。
```php
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($val = 0, $left = null, $right = null) {
 *         $this->val = $val;
 *         $this->left = $left;
 *         $this->right = $right;
 *     }
 * }
 */
class Solution {

    /**
     * @param TreeNode $root
     * @return Boolean
     */
    function isBalanced($root) {
        [$_, $flag] = $this->dfs($root);
        return $flag;
    }

    function dfs($root) {
        if ($root == null) {
            return [0, true];
        }
        [$leftHeight, $leftFlag] = $this->dfs($root->left);
        [$rightHeight, $rightFlag] = $this->dfs($root->right);

        if (!$leftFlag || !$rightFlag) {
            return [null, false];
        }

        if (abs($leftHeight - $rightHeight) > 1) {
            return [null, false];
        } else {
            return [max($leftHeight, $rightHeight)+1, true];
        }
    }
}
```

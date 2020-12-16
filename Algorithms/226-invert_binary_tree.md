# 226. Invert Binary Tree

- 完成时间：2020-12-16
- 原题地址：https://leetcode.com/problems/invert-binary-tree/

## 题目描述

Invert a binary tree.

## 我的解法

### 递归实现
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
     * @return TreeNode
     */
    function invertTree($root) {
        if ($root == null) {
            return $root;
        }

        $leftChild = $this->invertTree($root->left);
        $rightChild = $this->invertTree($root->right);

        $root->right = $leftChild;
        $root->left = $rightChild;

        return $root;
    }
}
```

### 非递归实现
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
     * @return TreeNode
     */
    function invertTree($root) {
        $nextLevel = [$root];

        while ($nextLevel) {
            $currentLevel = $nextLevel;
            $nextLevel = [];
            while ($currentLevel) {
                $node = array_shift($currentLevel);
                $tmp = $node->left;
                $node->left = $node->right;
                $node->right = $tmp;
                if ($node->left) {
                    $nextLevel[] = $node->left;
                }
                if ($node->right) {
                    $nextLevel[] = $node->right;
                }
            }
        }

        return $root;
    }
}
```

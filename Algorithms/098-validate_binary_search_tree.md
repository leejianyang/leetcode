# 98. Validate Binary Search Tree

- 完成时间：2020-12-17
- 原题地址：https://leetcode.com/problems/validate-binary-search-tree/

## 题目描述

Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:
- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than the node's key.
- Both the left and right subtrees must also be binary search trees.

## 我的解法

### 非递归解法

使用中序遍历的方式遍历二叉树，如果这棵树是二叉查找树，那么它的中序遍历必定是单调递增的。
```php
class Solution {

    /**
     * @param TreeNode $root
     * @return Boolean
     */
    function isValidBST($root) {
        $nodes = [];
        $stack = [$root];

        while ($stack) {
            $top = array_pop($stack);
            if ($top->left) {
                $tmp = $top->left;
                $top->left = null;
                $stack[] = $top;
                $stack[] = $tmp;
            } else {
                if (count($nodes) && $top->val <= $nodes[count($nodes)-1]) {
                    return false;
                } else {
                    $nodes[] = $top->val;
                }
                if ($top->right) {
                    $stack[] = $top->right;
                }
            }
        }

        return true;
    }
}
```

#### 官方给出来的另一个非递归解法
```php
class Solution {

    /**
     * @param TreeNode $root
     * @return Boolean
     */
    function isValidBST($root) {
        $stack = [];
        $prev = null;

        while ($stack || $root) {
            while ($root) {
                $stack[] = $root;
                $root = $root->left;
            }
            $root = array_pop($stack);
            if ($prev !== null && $prev >= $root->val) {
                return false;
            }
            $prev = $root->val;
            $root = $root->right;
        }

        return true;
    }
}
```

### 递归解法
```php
class Solution {

    /**
     * @param TreeNode $root
     * @return Boolean
     */
    function isValidBST($root) {
        return $this->dfs($root, -INF, INF);
    }

    function dfs($node, $minVal, $maxVal) {
        if ($node == null) {
            return true;
        }

        if ($node->val <= $minVal || $node->val >= $maxVal) {
            return false;
        }

        return $this->dfs($node->left, $minVal, $node->val) && $this->dfs($node->right, $node->val, $maxVal);
    }
}
```

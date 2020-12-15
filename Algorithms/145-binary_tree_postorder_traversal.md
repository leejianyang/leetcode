# 145. Binary Tree Postorder Traversal

- 完成时间：2020-12-15
- 原题地址：https://leetcode.com/problems/binary-tree-postorder-traversal/

## 题目描述

Given the root of a binary tree, return the postorder traversal of its nodes' values.

Recursive solution is trivial, could you do it iteratively?

## Example

```
Input: root = [1,null,2,3]
Output: [3,2,1]
```

```
Input: root = [1,2]
Output: [2,1]
```

```
Input: root = [1,null,2]
Output: [2,1]
```

## 我的解法

二叉树的后序遍历：先遍历左子树，再遍历右子树，最后访问根节点

### 非递归解法
利用栈来实现非递归解法。
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
     * @return Integer[]
     */
    function postorderTraversal($root) {
        if ($root == null) {
            return [];
        }
        $stack = [];
        $result = [];
        $stack[] = $root;

        while ($stack) {
            $top = array_pop($stack);
            array_unshift($result, $top->val);
            if ($top->left) {
                $stack[] = $top->left;
            }
            if ($top->right) {
                $stack[] = $top->right;
            }
        }

        return $result;
    }
}
```

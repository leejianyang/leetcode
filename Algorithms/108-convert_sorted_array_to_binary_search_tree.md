# 108. Convert Sorted Array to Binary Search Tree

- 完成时间：2020-12-17
- 原题地址：https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/

## 题目描述

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

## Example
```
Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:
```

## 我的解法
利用二分法加递归构建二叉平衡搜索树
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
     * @param Integer[] $nums
     * @return TreeNode
     */
    function sortedArrayToBST($nums) {
        return $this->buildTree($nums, 0, count($nums)-1);
    }

    function buildTree($nums, $low, $high) {
        if ($low > $high) {
            return null;
        }

        $mid = intval(floor(($low + $high) / 2));

        $node = new TreeNode();
        $node->val = $nums[$mid];
        $node->left = $this->buildTree($nums, $low, $mid-1);
        $node->right = $this->buildTree($nums, $mid+1, $high);

        return $node;
    }
}
```

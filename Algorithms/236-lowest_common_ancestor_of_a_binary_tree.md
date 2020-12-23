# 236. Lowest Common Ancestor of a Binary Tree

- 完成时间：2020-12-23
- 原题地址：https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

## 题目描述

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

## Example

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```

## 我的解法
```php
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($value) { $this->val = $value; }
 * }
 */

class Solution {
    /**
     * @param TreeNode $root
     * @param TreeNode $p
     * @param TreeNode $q
     * @return TreeNode
     */
    function lowestCommonAncestor($root, $p, $q) {
        if ($root === null || $root->val == $p->val || $root->val == $q->val) {
            return $root;
        }

        $left = $this->lowestCommonAncestor($root->left, $p, $q);
        $right = $this->lowestCommonAncestor($root->right, $p, $q);
        if ($left && $right) {
            return $root;
        }

        if ($left) {
            return $left;
        } elseif ($right) {
            return $right;
        } else {
            return null;
        }
    }
}
```

自顶向下查找，只要找到 p 或 q 其中一个，就停止向下查找往上返回。假设一个节点 n，在它的左孩子或右孩子中找到了 p 或 q 其中一个，那么要么 p 或 q 是目标（最低共同祖先），要么目标节点在其余的分支里面。

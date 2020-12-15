# 144. Binary Tree Preorder Traversal

- 完成时间：2020-12-15
- 原题地址：https://leetcode.com/problems/binary-tree-preorder-traversal/

## 题目描述

Given the root of a binary tree, return the preorder traversal of its nodes' values.

Recursive solution is trivial, could you do it iteratively?

## Example
```
Input: root = [1,null,2,3]
Output: [1,2,3]
```

```
Input: root = []
Output: []
```

```
Input: root = [1,2]
Output: [1,2]
```

```
Input: root = [1,null,2]
Output: [1,2]
```

## 我的解法

树的前缀遍历：先访问根，接着访问左子树，再访问右子树。

### 非递归实现
利用栈结构可以实现数的前缀遍历，算法如下：
（1）将数的根节点入栈
（2）栈顶元素 top 出栈，将值记录进结果数组中
（3）若 top 有右孩子，将右孩子入栈
（4）若 top 有左孩子，将左孩子入栈
重复以上（2）、（3）、（4）直到栈空了为止。

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
    function preorderTraversal($root) {
        if ($root == null) {
            return [];
        }

        $result = [];
        $stack = [];
        $stack[] = $root;

        while ($stack) {
            $top = array_pop($stack);
            $result[] = $top->val;
            if ($top->right) {
                $stack[] = $top->right;
            }
            if ($top->left) {
                $stack[] = $top->left;
            }
        }

        return $result;
    }
}
```

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
     * @return Integer[]
     */
    function preorderTraversal($root) {
        if ($root == null) {
            return [];
        }

        $result = [$root->val];
        $result = array_merge($result, $this->preorderTraversal($root->left));
        $result = array_merge($result, $this->preorderTraversal($root->right));

        return $result;
    }
}
```

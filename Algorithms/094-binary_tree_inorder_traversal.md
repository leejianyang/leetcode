# 94. Binary Tree Inorder Traversal

- 完成时间：2020-12-16
- 原题地址：https://leetcode.com/problems/binary-tree-inorder-traversal/

Given the root of a binary tree, return the inorder traversal of its nodes' values.

Recursive solution is trivial, could you do it iteratively?

## Example

```
Input: root = [1,null,2,3]
Output: [1,3,2]
```

```
Input: root = []
Output: []
```

```
Input: root = [1,null,2]
Output: [1,2]
```

## 我的解法

数的中序遍历：先访问左子树，再访问根，最后访问右子树

### 非递归解法

利用栈结构
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
    function inorderTraversal($root) {
        $stack = [];
        $result = [];
        $stack[] = $root;

        while ($stack) {
            $top = array_pop($stack);
            if ($top->left) {
                $leftChild = $top->left;
                $top->left = null;
                $stack[] = $top;
                $stack[] = $leftChild;
            } else {
                $result[] = $top->val;
                if ($top->right) {
                    $stack[] = $top->right;
                }
            }
        }

        return $result;
    }
}
```

先将根节点入栈，然后循环执行出栈过程，直至栈为空。每次取出栈顶元素 $top 时：
- 若 $top 左孩子为空：
    - 意味着不需要再访问它的左子树，那么就把它自身的值写入结果数组 $result
    - 且若它的右孩子不为空，则把它的右孩子入栈
- 若 $top 左孩子不为空：
    - 意味着需要先访问它的左子树，那么就把它的左子树取出来放在别的变量 $leftChild 中，同时把 $top 左孩子置空
    - 将栈顶元素自身重新入栈（因为已经将它的左孩子置空了，下次再取出来的时候就不会重复访问其左孩子了）
    - 将栈顶元素的左孩子（即临时变量 $leftChild）入栈

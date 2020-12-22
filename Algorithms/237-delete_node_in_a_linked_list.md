# 237.Delete Node in a Linked List

- 完成时间: 2020-12-21
- 原题地址: https://leetcode.com/problems/delete-node-in-a-linked-list/

## 题目描述

Write a function to delete a node in a singly-linked list. You will not be given access to the head of the list, instead you will be given access to the node to be deleted directly.

It is guaranteed that the node to be deleted is not a tail node in the list.

## Example

```
Input: head = [4,5,1,9], node = 5
Output: [4,1,9]
Explanation: You are given the second node with value 5, the linked list should become 4 -> 1 -> 9 after calling your function.
```

```
Input: head = [4,5,1,9], node = 1
Output: [4,5,9]
Explanation: You are given the third node with value 1, the linked list should become 4 -> 5 -> 9 after calling your function.
```

## 解法

这题我解不出来 >.< 这题是一道非常异类的链表题，通常链表题都会给出表头节点，但这题没有。所以这道题的解法也非常刁钻，有点脑筋急转弯的意思。
我完成的时候（2020-12-21)，这题收获的 like 数量是2115， dislike 的数量是 8241，所以这道题争议很大。

其实就是两行代码的事情：
```php
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val) { $this->val = $val; }
 * }
 */

class Solution {
    /**
     * @param ListNode $node
     * @return
     */
    function deleteNode($node) {
        $node->val = $node->next->val;
        $node->next = $node->next->next;
    }
}
```

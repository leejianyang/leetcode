# 21. Merge Two Sorted Lists

完成时间：2020-12-02

原题地址：https://leetcode.com/problems/merge-two-sorted-lists/

## 题目描述

Merge two sorted linked lists and return it as a new sorted list. The new list should be made by splicing together the nodes of the first two lists.

## Example

```
Input: l1 = [1,2,4], l2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

```
Input: l1 = [], l2 = []
Output: []
```

```
Input: l1 = [], l2 = [0]
Output: [0]
```

## 我的解法
```php
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val = 0, $next = null) {
 *         $this->val = $val;
 *         $this->next = $next;
 *     }
 * }
 */
class Solution {

    /**
     * @param ListNode $l1
     * @param ListNode $l2
     * @return ListNode
     */
    function mergeTwoLists($l1, $l2) {
        $head = null;
        $tail = null;

        while ($l1 && $l2) {
            if ($l1->val < $l2->val) {
                $current = $l1;
                $l1 = $current->next;
            } else {
                $current = $l2;
                $l2 = $current->next;
            }

            if ($head == null) {
                $head = $current;
                $tail = $current;
            } else {
                $tail->next = $current;
                $tail = $tail->next;
            }

            $tail->next = null;
        }

        if ($l1) {
            if ($head == null) {
                $head = $l1;
            } else {
                $tail->next = $l1;
            }
        }
        if ($l2) {
            if ($head == null) {
                $head = $l2;
            } else {
                $tail->next = $l2;
            }
        }

        return $head;
    }
}
```

# 83. Remove Duplicates from Sorted List

完成时间：2020-12-03

原题地址：https://leetcode.com/problems/remove-duplicates-from-sorted-list/

## 题目描述

Given a sorted linked list, delete all duplicates such that each element appear only once.

## Example

```
Input: 1->1->2
Output: 1->2
```

```
Input: 1->1->2->3->3
Output: 1->2->3
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
     * @param ListNode $head
     * @return ListNode
     */
    function deleteDuplicates($head) {
        $next = $head->next;
        $current = $head;

        while ($next) {
            if ($current->val == $next->val) {
                $next = $next->next;
                $current->next = $next;
            } else {
                $current = $next;
                $next = $next->next;
            }    
        }

        return $head;
    }
}
```

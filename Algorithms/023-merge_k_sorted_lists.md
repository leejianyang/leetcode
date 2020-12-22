# 23. Merge k Sorted Lists

- 完成时间：2020-12-21
- 原题地址：https://leetcode.com/problems/merge-k-sorted-lists/

## 题目描述

You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

## Example

```
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
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
     * @param ListNode[] $lists
     * @return ListNode
     */
    function mergeKLists($lists) {
        $result = null;
        $prev = null;
        $finished = false;

        while (!$finished) {
            //var_dump($lists);
            $finished = true;
            $minVal = null;
            $minIndex = null;

            for ($i = 0; $i < count($lists); $i++) {
                $lst = $lists[$i];
                if ($lst !== null) {
                    $finished = false;
                    if ($minIndex === null) {
                        $minIndex = $i;
                        $minVal = $lst->val;
                    } else {
                        if ($lst->val < $minVal) {
                            $minIndex = $i;
                            $minVal = $lst->val;
                        }
                    }
                }
            }

            if ($minIndex !== null) {
                $lst = $lists[$minIndex];
                $tmp = $lst;
                $lst = $lst->next;
                $lists[$minIndex] = $lst;
                if ($prev) {
                    $prev->next = $tmp;
                } else {
                    $result = $tmp;
                }
                $prev = $tmp;
            }
        }

        return $result;
    }
}
```

以上方法勉强能接解出来，就是效率比较差。

## 更优的解法

### 利用最小堆
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
     * @param ListNode[] $lists
     * @return ListNode
     */
    function mergeKLists($lists) {
        $heap = new SplMinHeap();

        foreach ($lists as $list) {
            $node = $list;
            while ($node) {
                $heap->insert($node->val);
                $node = $node->next;
            }
        }

        $resultHead = null;
        $prev = null;

        while (!$heap->isEmpty()) {
            $val = $heap->extract();
            $node = new ListNode($val);

            if ($prev) {
                $prev->next = $node;
            } else {
                $resultHead = $node;
            }
            $prev = $node;
        }

        return $resultHead;
    }
}
```

### 利用分治法
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
     * @param ListNode[] $lists
     * @return ListNode
     */
    function mergeKLists($lists) {
        if (count($lists) == 0) {
            return [];
        }

        while (count($lists) > 1) {
            $nextRound = [];
            $i = 0;
            while ($i < count($lists)) {
                if (($i + 1) < count($lists)) {
                    $nextRound[] = $this->merge($lists[$i], $lists[$i+1]);
                } else {
                    $nextRound[] = $lists[$i];
                }
                $i = $i + 2;
            }
            $lists = $nextRound;
        }

        return $lists[0];
    }

    function merge($l1, $l2) {
        $result = null;
        $prev = null;

        while ($l1 && $l2) {
            if ($l1->val < $l2->val) {
                $tmp = $l1;
                $l1 = $l1->next;
            } else {
                $tmp = $l2;
                $l2 = $l2->next;
            }
            if ($prev) {
                $prev->next = $tmp;
            } else {
                $result = $tmp;
            }
            $prev = $tmp;
        }

        if ($l1) {
            if ($prev) {
                $prev->next = $l1;
            } else {
                $result = $l1;
            }
        }
        if ($l2) {
            if ($prev) {
                $prev->next = $l2;
            } else {
                $result = $l2;
            }
        }

        return $result;
    }
}
```

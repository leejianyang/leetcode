# 138. Copy List with Random Pointer

- 完成时间: 2020-12-21
- 原题地址: https://leetcode.com/problems/copy-list-with-random-pointer/

## 题目描述

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

The Linked List is represented in the input/output as a list of n nodes. Each node is represented as a pair of [val, random_index] where:
- val: an integer representing Node.val
- random_index: the index of the node (range from 0 to n-1) where random pointer points to, or null if it does not point to any node.

## Example

```
Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]
```

```
Input: head = [[1,1],[2,1]]
Output: [[1,1],[2,1]
```

```
Input: head = [[3,null],[3,0],[3,null]]
Output: [[3,null],[3,0],[3,null]]
```

## 我的解法

```php
/**
 * Definition for a Node.
 * class Node {
 *     public $val = null;
 *     public $next = null;
 *     public $random = null;
 *     function __construct($val = 0) {
 *         $this->val = $val;
 *         $this->next = null;
 *         $this->random = null;
 *     }
 * }
 */

class Solution {
    /**
     * @param Node $head
     * @return Node
     */
    function copyRandomList($head) {
        // 记录旧链表中节点id与新节点的对应关系 (id => Node)
        $oldToNewMap = [];
        $prev = null;
        $newHead = null;

        // 第一遍遍历先复制节点
        $oldNode = $head;
        while ($oldNode) {
            $node = new Node($oldNode->val);
            if ($prev == null) {
                $prev = $node;
                $newHead = $node;
            } else {
                $prev->next = $node;
            }
            $oldToNewMap[spl_object_hash($oldNode)] = $node;

            $oldNode = $oldNode->next;
            $prev = $node;
        }

        // 第二遍遍历复制 random 指针
        $newNode = $newHead;
        $oldNode = $head;
        while ($oldNode) {
            if ($oldNode->random) {
                $child = $oldToNewMap[spl_object_hash($oldNode->random)];
                $newNode->random = $child;
            }

            $oldNode = $oldNode->next;
            $newNode = $newNode->next;
        }

        return $newHead;
    }
}
```

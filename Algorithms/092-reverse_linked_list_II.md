# 92. Reverse Linked List II

- 完成时间：2020-09-17
- 原题地址：https://leetcode.com/problems/reverse-linked-list-ii/

## 题目描述

Reverse a linked list from position *m* to *n*. Do it in one-pass.

**Note:** 1 ≤ *m* ≤ *n* ≤ length of list.

## Example

```
Input: 1->2->3->4->5->NULL, m = 2, n = 4
Output: 1->4->3->2->5->NULL
```

## 我的解法

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """
        reversed_head = head
        first_part_tail = None
        for i in range(m-1):
            first_part_tail = reversed_head
            reversed_head = reversed_head.next
        
        reversed_tail = reversed_head
        next_node = reversed_head.next
        for i in range(n-m):
            tmp = reversed_head
            reversed_head = next_node
            next_node = next_node.next
            reversed_head.next = tmp

        reversed_tail.next = next_node
        if first_part_tail:
            first_part_tail.next = reversed_head
            return head
        else:
            return reversed_head
```


# 143. Reorder List

完成时间：2019-12-09

原题地址：https://leetcode.com/problems/reorder-list/

## 题目描述

Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You may not modify the values in the list's nodes, only nodes itself may be changed.

## Example
Example 1:
```
Given 1->2->3->4, reorder it to 1->4->2->3.
```
Example 2:
```
Given 1->2->3->4->5, reorder it to 1->5->2->4->3.
```

## 我的解法
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reorderList(self, head):
        """
        :type head: ListNode
        :rtype: None Do not return anything, modify head in-place instead.
        """
        if not head:
            return head
        lst = head.next
        head.next = None
        
        reversed_list, total_node = self.reverse(lst)
        cursor = head
        for _ in xrange(0, int(math.ceil(total_node / 2.0))):
            cursor.next = reversed_list
            cursor = cursor.next
            reversed_list = reversed_list.next
        cursor.next = None
        
        lst, _ = self.reverse(reversed_list)
        cursor = head.next
        while lst:
            tmp = lst.next
            lst.next = cursor.next
            cursor.next = lst
            if lst.next == None:
                lst = tmp
                break
            cursor = lst.next
            lst = tmp
        if lst is not None:
            cursor.next = lst
        
		
    def reverse(self, lst):
        '''
        将链表翻转
        '''
        head = None
        node_count = 0

        while lst:
            node_count += 1
            tmp = lst.next
            lst.next = head
            head = lst
            lst = tmp
        return head, node_count
        
```
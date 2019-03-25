# 24. Swap Nodes in Pairs

完成时间：2019-03-25

原题：https://leetcode.com/problems/swap-nodes-in-pairs/

## 题目描述

Given a linked list, swap every two adjacent nodes and return its head.

You may not modify the values in the list's nodes, only nodes itself may be changed.

## Example

```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```

## 我的首个 AC
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head is None or head.next is None:
            return head
        
        first_node = head
        second_node = head.next
        head = second_node
        
        tmp_head = ListNode(None)
        
        while True:
            tmp_head.next = second_node
            first_node.next = second_node.next
            second_node.next = first_node
            
            tmp_head = first_node
            first_node = first_node.next
            if first_node is None:
                break
            second_node = first_node.next
            if second_node is None:
                break
        
        return head
```
# 148. Sort List

完成时间：2019-04-04
原题：https://leetcode.com/problems/sort-list/

## 题目描述

Sort a linked list in O(n log n) time using constant space complexity.

## Example
```
Input: 4->2->1->3
Output: 1->2->3->4
```

```
Input: -1->5->3->4->0
Output: -1->0->3->4->5
```

## 我的首个 AC
利用了归并排序的思想
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def sortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        length = self.getListLength(head)
        return self.devideList(head, length)
    
    def devideList(self, head, length):
        if length <= 1:
            return head
        
        left_part_length = length / 2
        right_part_length = length - length / 2
        left_part_head = head
        right_part_head = self.getMiddleNode(head, length)
        
        node = left_part_head
        for _ in range(left_part_length-1):
            node = node.next
        node.next = None
        
        node = right_part_head
        for _ in range(right_part_length-1):
            node = node.next
        node.next = None
                
        left_part = self.devideList(left_part_head, left_part_length)
        right_part = self.devideList(right_part_head, right_part_length)
        
        return self.merge(left_part, right_part)
        
    def merge(self, left_part, right_part):
        head = None
        current = None
        
        left_node = left_part
        right_node = right_part
        
        while left_node is not None and right_node is not None:
            if left_node.val <= right_node.val:
                if head is None:
                    head = left_node
                    current = head
                else:
                    current.next = left_node
                    current = current.next
                left_node = left_node.next
            else:
                if head is None:
                    head = right_node
                    current = head
                else:
                    current.next = right_node
                    current = current.next
                right_node = right_node.next

        if left_node:
            if head is None:
                head = left_node
            else:
                current.next = left_node
        elif right_node:
            if head is None:
                head = right_node
            else:
                current.next = right_node
                        
        return head
        
    
    def getListLength(self, head):
        count = 0
        node = head
        
        while node is not None:
            count += 1
            node = node.next
        
        return count
    
    def getMiddleNode(self, head, length):
        middle = length / 2
        node = head
        
        for _ in xrange(middle):
            node = node.next
            
        return node
```
# 82. Remove Duplicates from Sorted List II

完成时间：2019-03-26

原题：https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/

## 题目描述

Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

## Example

```
Input: 1->2->3->3->4->4->5
Output: 1->2->5
```

```
Input: 1->1->1->2->3
Output: 2->3
```

## 我的首个 AC
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head is None:
            return None
        
        this_round_head = None
        this_round_first = head
        this_round_last = head
        
        while True:
            # 每次都找相同数据的最长子串
            while True:
                if this_round_last.next is None:
                    break
                if this_round_last.next.val != this_round_first.val:
                    break
                this_round_last = this_round_last.next
            
            if this_round_first == this_round_last:
                if this_round_head is None:
                    this_round_head = this_round_first
                    head = this_round_first
                else:
                    this_round_head.next = this_round_first
                    this_round_head = this_round_first
                this_round_first = this_round_first.next
                this_round_last = this_round_first
                if this_round_first is None:
                    break
            else:
                if this_round_head is None:
                    pass
                else:
                    this_round_head.next = this_round_last.next
                this_round_first = this_round_last.next
                this_round_last = this_round_last.next
                if this_round_first is None:
                    break
        if this_round_head is None:
            return None
        return head
```
# 142. Linked List Cycle II

- 完成时间：2020-09-11
- 原题地址：https://leetcode.com/problems/linked-list-cycle-ii/

## 题目描述

Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.

Note: Do not modify the linked list.

## 我的解法
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def detectCycle(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        slow_pointer = head
        fast_pointer = head
        # 判断链表中是否存在环
        while fast_pointer is not None and fast_pointer.next is not None:
            slow_pointer = slow_pointer.next
            fast_pointer = fast_pointer.next.next
            if slow_pointer == fast_pointer:
                break
        else:
            return None
        # 计算环的大小：cycle_size
        fast_pointer = slow_pointer.next
        cycle_size = 1
        while fast_pointer != slow_pointer:
            fast_pointer = fast_pointer.next
            cycle_size += 1
        # 将两个指针都重置回头部，接着将两个指针拉开 cycle_size 的距离，然后两个指针一齐向前走，相遇的位置则为环的开始位置
        slow_pointer = head
        fast_pointer = head
        while cycle_size > 0:
            fast_pointer = fast_pointer.next
            cycle_size -= 1

        while slow_pointer != fast_pointer:
            slow_pointer = slow_pointer.next
            fast_pointer = fast_pointer.next

        return slow_pointer
```

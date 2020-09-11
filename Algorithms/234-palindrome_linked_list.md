# 234. Palindrome Linked List
- 完成时间: 2020-09-11
- 原题地址: https://leetcode.com/problems/palindrome-linked-list/

## 题目描述
Given a singly linked list, determine if it is a palindrome.

Follow up:
Could you do it in O(n) time and O(1) space?

## Example
```
Input: 1->2
Output: false
```

```
Input: 1->2->2->1
Output: true
```

## 我的解法
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        if head is None:
            return True
        if head.next is None:
            return True

        first_half = head
        second_half_head = self.find_the_second_half(head)
        second_half = self.reverse_second_half(second_half_head)

        while second_half is not None:
            if second_half.val != first_half.val:
                return False
            second_half = second_half.next
            first_half = first_half.next

        return True

    def find_the_second_half(self, head):
        slow_pointer = head
        fast_pointer = head

        while fast_pointer.next is not None and fast_pointer.next.next is not None:
            slow_pointer = slow_pointer.next
            fast_pointer = fast_pointer.next.next

        return slow_pointer.next

    def reverse_second_half(self, head):
        a = head
        tail = head
        b = a.next
        while b is not None:
            head = b
            b = b.next
            head.next = a
            a = head
        tail.next = None
        return head
```

先找出链表的中间点，接着翻转链表的后半部分，最后遍历对比一次前半部分和后半部分看是否存在差异。

# 876. Middle of the Linked List
- 完成时间：2020-09-11
- 原题地址：https://leetcode.com/problems/middle-of-the-linked-list/

## 题目描述
Given a non-empty, singly linked list with head node head, return a middle node of linked list.

If there are two middle nodes, return the second middle node.

Note:
- The number of nodes in the given list will be between 1 and 100.

## Example
```
Input: [1,2,3,4,5]
Output: Node 3 from this list (Serialization: [3,4,5])
The returned node has value 3.  (The judge's serialization of this node is [3,4,5]).
Note that we returned a ListNode object ans, such that:
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, and ans.next.next.next = NULL.
```

```
Input: [1,2,3,4,5,6]
Output: Node 4 from this list (Serialization: [4,5,6])
Since the list has two middle nodes with values 3 and 4, we return the second one.
```

## 我的解法
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def middleNode(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        slow_pointer = head
        fast_pointer = head

        while fast_pointer.next is not None and fast_pointer.next.next is not None:
            slow_pointer = slow_pointer.next
            fast_pointer = fast_pointer.next.next

        if fast_pointer.next is None:
            return slow_pointer
        else:
            return slow_pointer.next
```

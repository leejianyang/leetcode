# Reverse Nodes in k-Group

完成时间：2019-10-29
原题目：https://leetcode.com/problems/reverse-nodes-in-k-group/

## 问题描述

Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

- Only constant extra memory is allowed.
- You may not alter the values in the list's nodes, only nodes itself may be changed.

## Example
```
Given this linked list: 1->2->3->4->5
For k = 2, you should return: 2->1->4->3->5
For k = 3, you should return: 3->2->1->4->5
```

## 我的首个 AC
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseKGroup(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        current_head = head
        new_head = None      
        last_round_tail = None

        while True:
            this_round_finished = False
            tmp_nodes = []
            cursor = current_head

            for _ in range(k):
                if cursor is None:
                    break
                else:
                    tmp_nodes.append(cursor)
                    cursor = cursor.next
            else:
                # find all k nodes
                current_tail = cursor

                i = k - 1
                while (i >= 0):
                    if i != 0:
                        tmp_nodes[i].next = tmp_nodes[i-1]
                    else:
                        tmp_nodes[i].next = current_tail
                    i -= 1
                this_round_finished = True

            # 到此完成了一趟循环
            if this_round_finished:
                current_head = tmp_nodes[0].next

                if new_head is None:
                    new_head = tmp_nodes[k-1]
                else:
                    last_round_tail.next = tmp_nodes[k-1]
                last_round_tail = tmp_nodes[0]
            else:
                break

        if new_head is not None:
            return new_head
        else:
            return head
```

## 其它的 solution

看了论坛里别人的解法后，尝试了一下递归的解法：
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseKGroup(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        current_head = head
        cursor = head
        
        for _ in range(k):
            if cursor is None:
                break
            cursor = cursor.next
        else:
            next_round_head = self.reverseKGroup(cursor, k)
            tail = next_round_head
            cursor = current_head
            
            for _ in range(k-1):    
                tmp = cursor.next
                cursor.next = tail
                tail = cursor
                cursor = tmp
            cursor.next = tail
            current_head = cursor
        
        return current_head
```
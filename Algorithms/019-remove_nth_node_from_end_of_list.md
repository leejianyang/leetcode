# 19. Remove Nth Node From End of List

完成时间：2019-03-13

原题：https://leetcode.com/problems/remove-nth-node-from-end-of-list/

## 题目描述

Given a linked list, remove the n-th node from the end of list and return its head.

Given n will always be valid.

### Follow Up

Could you do this in one pass?

## Example

```
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```

## 我的首个 AC

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        point_list = []
        current_node = head
        
        while current_node is not None:
            point_list.append(current_node)
            current_node = current_node.next
        
        remove_index = len(point_list) - n
        if remove_index == 0:
            # 要去掉的是头节点
            if len(point_list) > 1:
                # 原始的链表不只1个元素
                return point_list[1]
            else:
                # 原始的链表只有1个元素
                return None
        else:
            if n == 1:
                # 去掉最后一个节点
                point_list[remove_index-1].next = None
                return head
            else:
                point_list[remove_index-1].next = point_list[remove_index+1]
                return head
```

## 官方 Solution

我的解法虽然也是一次遍历链表，但是额外使用的指针较多。官方给出的「One pass algorithm」只需要使用2个额外的指针。

将指针 1 和指针 2 的间距设置为 n+2，若指针 1 到达链表末端时，指针 2 指向的就是要移除的节点的上一个节点。
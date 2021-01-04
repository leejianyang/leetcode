# 206. Reverse Linked List
- 完成时间：2020-09-16
- 原题地址：https://leetcode.com/problems/reverse-linked-list/

## 题目描述
Reverse a singly linked list.

Follow up:

A linked list can be reversed either iteratively or recursively. Could you implement both?

## Example
```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

## 我的解法

### 遍历解法
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head is None:
            return head
        tail = head
        next_node = head.next
        while next_node:
            tmp = next_node.next
            next_node.next = head
            head = next_node
            next_node = tmp
        tail.next = None
        return head
```

### 递归解法
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head is None:
            return None
        [head, tail] = self.reverse(head)
        tail.next = None
        return head

    def reverse(self, node):
        if node.next is None:
            return [node, node]
        head, tail = self.reverse(node.next)
        tail.next = node
        return [head, node]
```

官方参考答案给出的递归解法：
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head is None or head.next is None:
            return head

        node = self.reverseList(head.next)
        head.next.next = head
        head.next = None
        return node
```

### go 语言版本
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseList(head *ListNode) *ListNode {
    if head == nil {
        return nil
    }

    head, tail := reverse(head)
    tail.Next = nil
    return head
}

func reverse(node *ListNode) (*ListNode, *ListNode) {
    if node.Next == nil {
        return node, node
    }
    head, tail := reverse(node.Next)
    tail.Next = node
    return head, node
}
```

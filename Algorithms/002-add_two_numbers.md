# 2. Add Two Numbers

完成时间：2019-03-08

原题：https://leetcode.com/problems/add-two-numbers

## 题目描述

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

## 示例

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

## 我的首个 accept
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        num1 = self.getNumber(l1)
        num2 = self.getNumber(l2)
        sum = num1 + num2
        return self.makeList(sum)
    
    def getNumber(self, l1):
        num = '';
        next_node = l1
        while next_node is not None:
            val = next_node.val
            num = num + str(val)
            next_node = next_node.next
        return int(num[::-1])
    
    def makeList(self, num):
        num = str(num)[::-1]
        head = None
        pre_node = None
        for item in num:
            node = ListNode(item)
            
            if head is None:
                head = node
            
            if pre_node is not None:
                pre_node.next = node
            
            pre_node = node
        
        return head
```

## 我的另一个解法

还可以不用翻转字符串，直接将两个链表逐位相加，获取结果，就好像从低位往高位加法运算那样：

```php
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val) { $this->val = $val; }
 * }
 */
class Solution {

    /**
     * @param ListNode $l1
     * @param ListNode $l2
     * @return ListNode
     */
    function addTwoNumbers($l1, $l2) {
        $l1NextNode = $l1;
        $l2NextNode = $l2;
        $result = null;
        $carry = 0;
        $resultPrviousNode = null;
        
        while ($l1NextNode != null || $l2NextNode != null) {
            $sum = ($l1NextNode->val ?? 0) + ($l2NextNode->val ?? 0) + $carry;
            $carry = intval($sum / 10);
            $unit = $sum % 10;
            
            $node = new ListNode($unit);
                
            if ($result === null) {
                $result = $node;
            }

            if ($resultPrviousNode !== null) {
                $resultPrviousNode->next = $node;
            }
            $resultPrviousNode = $node;
            
            $l1NextNode = $l1NextNode->next;
            $l2NextNode = $l2NextNode->next;
        }
        
        $sum = ($l1NextNode->val ?? 0) + ($l2NextNode->val ?? 0) + $carry;
        $carry = intval($sum / 10);
        $unit = $sum % 10;
        if ($unit) {
            $node = new ListNode($unit);
            $resultPrviousNode->next = $node;
            $resultPrviousNode = $node;
        }
        if ($carry) {
            $node = new ListNode($unit);
            $resultPrviousNode->next = $node;
        }
        
        return $result;
    }
}
```
# 239. Sliding Window Maximum

完成时间：2019-11-01

原题地址：https://leetcode.com/problems/sliding-window-maximum/

## 题目描述

Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

Note:
You may assume k is always valid, 1 ≤ k ≤ input array's size for non-empty array.

Follow up:
Could you solve it in linear time?

## Example

```
Input: nums = [1,3,-1,-3,5,3,6,7], and k = 3
Output: [3,3,5,5,6,7] 
Explanation: 

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

## 我的首个解法
```python
class Node(object):
    pass
    
class Solution(object):
    
    def maxSlidingWindow(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        self.output = []
        self.queue = []
        
        for val in nums:
            inserted = self.insert_from_head(val)
            if not inserted:
                self.insert_from_tail(val)
            self.add_output(k)
        self.add_output(k)
        
        return self.output
            
    def insert_from_head(self, val):
        if len(self.queue) == 0:
            node = Node()
            node.front = 0
            node.back = 0
            node.val = val
            self.queue.append(node)
            return True
        else:
            head = self.queue[0]
            if val <= head.val:
                head.back += 1
                return False
            else:
                node = Node()
                node.val = val
                node.front = head.front + head.back + 1
                node.back = 0
                self.queue = []
                self.queue.append(node)
                return True
    
    def insert_from_tail(self, val):
        node = Node()
        node.val = val
        node.back = 0
        node.front = 0
        while True:
            if len(self.queue) == 1:
                self.queue.append(node)
                return True
            tail = self.queue[-1]    
            if tail.val >= val:
                i = len(self.queue) - 1
                while i > 0:
                    self.queue[i].back += 1
                    i -= 1
                self.queue.append(node)
                return True
            else:
                node.front += tail.front + 1
                self.queue.pop(-1)
    
    def add_output(self, k):
        if len(self.queue) == 0:
            return
        head = self.queue[0]
        if (head.front + head.back) >= (k - 1):
            self.output.append(head.val)
            if head.back == (k - 1):
                self.queue.pop(0)
            else:
                head.front -= 1
```

内存使用量非常少，数据显示「 less than 100.00% of Python online submissions」:)

我的想法是，用一个双端队列存储所有可能成为窗口最大值的数。例如 k=4，如果 input 的第 3 个元素比前两个元素大，那么前2个元素永远不可能成为某个窗口的最大值，它们就可以舍弃掉了。然后第4个元素比第三个元素小的话，由于它位于第3个元素的后面，所以先不能把它舍弃，先放在队尾；如果第5个元素比第4个元素大，那么第4个元素就可以舍弃，把第5个元素放入队尾。

## 更优的解法

看了讨论区里面别人的解法，总结称这类题目为「monotonic queue」，即队列里面的元素是单调递减的，其实跟我的方案差不多，只是我搞得太复杂了。

解法如下：
```python
class Deque(object):
    
    def __init__(self):
        self.deque = []
    
    def push(self, val):
        node = [val, 0]
        if len(self.deque) > 0 and self.deque[-1][0] < val:
            node = [val, self.deque[-1][1] + 1]
            self.deque.pop(-1)
        self.deque.append(node)
    
    def pop(self):
        if self.deque[0][1] > 0:
            self.deque[0][1] -= 1
            return
        self.deque.pop(0)
    
    def max(self):
        return self.deque[0][0]


class Solution(object):

    def maxSlidingWindow(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        output = []
        deque = Deque()
        
        for i in xrange(k-1):
            deque.push(nums[i])
        
        i = k - 1
        while i < len(nums):
            deque.push(nums[i])
            output.append(deque.max())
            deque.pop()
            i += 1
        
        return output
```
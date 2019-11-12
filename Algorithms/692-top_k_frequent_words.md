# 692. Top K Frequent Words

完成时间：2019-11-7

原题地址：https://leetcode.com/problems/top-k-frequent-words/

## 题目描述

Given a non-empty list of words, return the k most frequent elements.

Your answer should be sorted by frequency from highest to lowest. If two words have the same frequency, then the word with the lower alphabetical order comes first.

Note:
- You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
- Input words contain only lowercase letters.

## Example

Example 1:
```
Input: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
Output: ["i", "love"]
Explanation: "i" and "love" are the two most frequent words.
    Note that "i" comes before "love" due to a lower alphabetical order.
```

Example 2:
```
Input: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
Output: ["the", "is", "sunny", "day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words,
    with the number of occurrence being 4, 3, 2 and 1 respectively.
```

## 我的首个解法
```python
class Node(object):
    def __init__(self, val):
        self.val = val
        self.children = {}
        self.frequency = 0

        
class Solution(object):
    def topKFrequent(self, words, k):
        """
        :type words: List[str]
        :type k: int
        :rtype: List[str]
        """
        root = Node('')
        for word in words:
            self.insert_trie(root, word)
        
        self.word_frequence_list = []
        self.traverse_trie(root, '')

        self.merge_sort(0, len(self.word_frequence_list)-1)
        result = []
        for item in self.word_frequence_list[:k]:
            result.append(item[0])
        return result
    
    def insert_trie(self, root, word):
        node = root
        for letter in word:
            if not letter in node.children:
                node.children[letter] = Node(letter)
            node = node.children[letter]
        node.frequency += 1
    
    def traverse_trie(self, node, prefix):
        if node.frequency > 0:
            word = prefix + node.val
            self.word_frequence_list.append((word, node.frequency))
        
        prefix = prefix + node.val
        if len(node.children) == 0:
            return
        
        keys = node.children.keys()
        keys.sort()
        
        for key in keys:
            self.traverse_trie(node.children[key], prefix)
    
    def merge_sort(self, start, end):
        if start >= end:
            return
        
        mid = (start + end) / 2
        self.merge_sort(start, mid)
        self.merge_sort(mid+1, end)
        
        self.merge(start, mid, end)
    
    def merge(self, start, mid, end):
        left_part = self.word_frequence_list[start:mid+1]
        right_part = self.word_frequence_list[mid+1:end+1]
        
        index = start
        left_index = 0
        right_index = 0
        while left_index < len(left_part) and right_index < len(right_part):
            if left_part[left_index][1] >= right_part[right_index][1]:
                self.word_frequence_list[index] = left_part[left_index]
                left_index += 1
                index += 1
            else:
                self.word_frequence_list[index] = right_part[right_index]
                right_index += 1
                index += 1
        
        while left_index < len(left_part):
            self.word_frequence_list[index] = left_part[left_index]
            left_index += 1
            index += 1
        
        while right_index < len(right_part):
            self.word_frequence_list[index] = right_part[right_index]
            right_index += 1
            index += 1
```
这个解法集合了 Trie 树和归并排序，可行，但是效率非常差 :(

主要是我为了保持字符串的字母顺序，直接将所有的单词构建成 Trie 树，代价太高。我只需将输入的 words 数组遍历一次，用一个字典记录下各个单词出现的次数，然后再放进优先队列里面就可以了。


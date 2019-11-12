# 212. World Search II

完成时间：2019-11-11

原题地址：https://leetcode.com/problems/word-search-ii/

## 题目描述

Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

Note:
1. All inputs are consist of lowercase letters a-z.
2. The values of words are distinct.

## Example

```
Input: 
board = [
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]
words = ["oath","pea","eat","rain"]

Output: ["eat","oath"]
```

## 我的首个solution
```python
class Node(object):
    def init(self):
        self.children = {}
        self.end_of_word = False

class Solution(object):
    """
    :type board: List[List[str]]
    :type words: List[str]
    :rtype: List[str]
    """
    def findWords(self, board, words):
        trie_tree_root = Node()
        self.output = set()
        self.board = board
        self.row_size = len(board)
        if self.row_size == 0:
            return []
        self.col_size = len(board[0])
        if self.col_size == 0:
            return []

        for word in words:
            node = trie_tree_root
            for letter in word:
                if letter not in node.children:
                    node.children[letter] = Node()
                node = node.children[letter]
            node.end_of_word = True
    
        for row in xrange(self.row_size):
            for col in xrange(self.col_size):
                self.match_world(row, col, trie_tree_root, set(), '')
        return self.output
    
    def match_world(self, row, col, node, coordinate_sequence, string):
        letter = self.board[row][col]
        if letter in node.children:
            string = string + letter
            if node.children[letter].end_of_word:
                self.output.add(string)
            coordinate_sequence.add((row, col))		# 存储当前组成字符串的路径
    
            # 上
            new_row = row - 1
            new_col = col
            if new_row >= 0:
                if (new_row, new_col) not in coordinate_sequence:
                    new_coordinate_sequence = coordinate_sequence.copy()
                    self.match_world(new_row, new_col, node.children[letter], new_coordinate_sequence, string)
            # 下
            new_row = row + 1
            new_col = col
            if new_row < self.row_size:
                if (new_row, new_col) not in coordinate_sequence:
                    new_coordinate_sequence = coordinate_sequence.copy()
                    self.match_world(new_row, new_col, node.children[letter], new_coordinate_sequence, string)
            # 左
            new_row = row
            new_col = col - 1
            if new_col >= 0:
                if (new_row, new_col) not in coordinate_sequence:
                    new_coordinate_sequence = coordinate_sequence.copy()
                    self.match_world(new_row, new_col, node.children[letter], new_coordinate_sequence, string)
            # 右
            new_row = row
            new_col = col + 1
            if new_col < self.col_size:
                if (new_row, new_col) not in coordinate_sequence:
                    new_coordinate_sequence = coordinate_sequence.copy()
                    self.match_world(new_row, new_col, node.children[letter], new_coordinate_sequence, string)

```

先将目标单词集构建成前缀树，然后逐个逐个遍历 board，若某个元素在树的第一层，则找它上下左右的元素是否在树的第二层，若符合，则再找前后左右的元素是否在树的第三层，如此类推。
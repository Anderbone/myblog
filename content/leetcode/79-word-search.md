+++
date = "2021-03-21"
title = "79. Word search"
tags = ["leetcode","backtracking"]
+++

Given a 2D board and a word, find if the word exists in the grid.
The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.
Example:
board = [ ['A','B','C','E'], ['S','F','C','S'], ['A','D','E','E'] ] Given word = "ABCCED", return true. Given word = "SEE", return true. Given word = "ABCB", return false

- code
```py
class Solution:
    
    def exist(self, board: List[List[str]], word: str) -> bool:
        count = collections.Counter(x for rows in board for x in rows)
        for c, cnt in collections.Counter(word).items():
            if cnt > count[c]:
                return False
            
        r = len(board)
        c = len(board[0])
        length = len(word)
        
        def go(x, y, index):
            if index == length:
                return True
            
            w = word[index]
            
            prev = board[x][y]
            board[x][y] = '' 
            
            if x > 0 and board[x - 1][y] == w and go(x - 1, y, index + 1):
                return True
            if x + 1 < r and board[x + 1][y] == w and go(x + 1, y, index + 1):
                return True
            if y > 0 and board[x][y - 1] == w and go(x, y - 1, index + 1):
                return True
            if y + 1 < c and board[x][y + 1] == w and go(x, y + 1, index + 1):
                return True
            
            board[x][y] = prev
            return False
        
        candidates = [(x, y) for x in range(r) for y in range(c) if board[x][y] == word[0]]
        
        return any(go(x, y, 1) for x, y in candidates)

```

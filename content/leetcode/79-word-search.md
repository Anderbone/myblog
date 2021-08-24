+++
date = "2021-03-21"
title = "79. Word search"
tags = ["leetcode","backtracking"]
+++

Given a 2D board and a word, find if the word exists in the grid.
The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.
Example:
board = [ ['A','B','C','E'], ['S','F','C','S'], ['A','D','E','E'] ] Given word = "ABCCED", return true. Given word = "SEE", return true. Given word = "ABCB", return false


```py
class Solution:
    
    def exist(self, board: List[List[str]], word: str) -> bool:

        count = collections.Counter(x for rows in board for x in rows)
        for c, cnt in collections.Counter(word).items():
            if cnt > count[c]:
                return False

        self.res = False
        self.word = word
        self.width = len(board[0])
        self.height = len(board)
        start_points = [(row,col) for row in range(self.height) 
        for col in range(self.width) if board[row][col] == word[0]]

        for x, y in start_points:
            board[x][y] = ""
            self.dfs(board, 1, x, y) # word[1] is next target
            board[x][y] = word[0]
        return self.res

    def dfs(self, board, word_index, x, y):
        if word_index == len(self.word):
            self.res = True
            return
        if x < 0 or y < 0 or x == self.height or y == self.width:
            return
        
        if x-1 >= 0 and board[x-1][y] == self.word[word_index]:
            board[x-1][y] = ""
            self.dfs(board, word_index+1, x-1, y)
            board[x-1][y] = self.word[word_index]
        
        if y-1 >= 0 and board[x][y-1] == self.word[word_index]:
            board[x][y-1] = ""
            self.dfs(board, word_index+1, x, y-1)
            board[x][y-1] = self.word[word_index]
        
        if x+1 < self.height and board[x+1][y] == self.word[word_index]:
            board[x+1][y] = ""
            self.dfs(board, word_index+1, x+1, y)
            board[x+1][y] = self.word[word_index]
        
        if y+1 < self.width and board[x][y+1] == self.word[word_index]:
            board[x][y+1] = ""
            self.dfs(board, word_index+1, x, y+1)
            board[x][y+1] = self.word[word_index]
```

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

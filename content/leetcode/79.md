+++ 
date = "2022-01-16"
title = "79. Word Search"
tags = ["backtracking"]
+++
[Word Search - LeetCode](https://leetcode.com/problems/word-search/)

Given an m x n grid of characters board and a string word, return true __if__ word __exists in the grid__.
The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.
 
Example 1:
![](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED" Output: true 

Example 2:
![](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE" Output: true 

Example 3:
![](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB" Output: false 
 
Constraints:

	m == board.length
	n = board[i].length
	1 <= m, n <= 6
	1 <= word.length <= 15
	board and word consists of only lowercase and uppercase English letters.
---
- code backtracking will return True or False
```py
class Solution:
    
    def exist(self, board: List[List[str]], word: str) -> bool:

        board_count = Counter(char for rows in board for char in rows)
        for word_char, need in Counter(word).items():
            if need > board_count[word_char]: return False

        m = len(board)
        n = len(board[0])

        def backtracking(x, y, index):
            if board[x][y] != word[index]: return False
            if index == len(word) - 1: return True
            
            pre = board[x][y]
            board[x][y] = ""
            
            for dx, dy in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
                nx, ny = x + dx, y + dy
                if 0 <= nx < m and 0 <= ny < n:
                    if backtracking(nx, ny, index + 1): return True

            board[x][y] = pre
            return False

        return any(backtracking(x, y, 0) for x in range(m) for y in range(n))

```
- code use self.res to return, backtracking has no return value
```py
class Solution:
    
    def exist(self, board: List[List[str]], word: str) -> bool:

        board_count = Counter(char for rows in board for char in rows)
        for word_char, need in Counter(word).items():
            if need > board_count[word_char]: return False

        m = len(board)
        n = len(board[0])
        
        self.res = False
        def backtracking(x, y, index):
            if board[x][y] != word[index]: return
            if index == len(word) - 1: 
                self.res = True
                return
            
            pre = board[x][y]
            board[x][y] = ""
            
            for dx, dy in [(1, 0), (-1, 0), (0, 1), (0, -1)]:
                nx, ny = x + dx, y + dy
                if 0 <= nx < m and 0 <= ny < n:
                    backtracking(nx, ny, index + 1)

            board[x][y] = pre

        for x in range(m):
            for y in range(n):
                backtracking(x, y, 0)
        
        return self.res
```

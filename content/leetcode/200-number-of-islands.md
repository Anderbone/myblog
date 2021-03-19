+++
date = "2021-03-13"
title = "200. Number of islands"
tags = ["leetcode","graph"]
+++

Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.
Example 1:
11110  
11010  
11000  
00000  

Output: 1 
- code
```py
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        island = 0
        self.grid = grid
        self.m = len(grid[0])
        self.n = len(grid)

        for row in range(self.n):
            for col in range(self.m):
                cur = self.grid[row][col]
                if cur == "1":
                    island += 1
                    self.removeConnected(row, col)
        return island
    
    def removeConnected(self, row, col):
        self.grid[row][col] = "0"
        if col - 1 > -1 and self.grid[row][col-1] == "1":
            self.removeConnected(row, col-1)
        if col + 1 < self.m and self.grid[row][col+1] == "1":
            self.removeConnected(row, col+1)
        if row - 1 > -1 and self.grid[row-1][col] == "1":
            self.removeConnected(row-1, col)
        if row + 1 < self.n and self.grid[row+1][col] == "1":
            self.removeConnected(row+1, col)

```

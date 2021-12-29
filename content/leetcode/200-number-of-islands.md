+++
date = "2021-03-13"
title = "200. Number of islands"
tags = ["graph"]
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
        self.m = len(grid)
        self.n = len(grid[0])
        count = 0

        for row in range(self.m):
            for col in range(self.n):
                if grid[row][col] == "1":
                    count += 1
                    self.dfs(grid, row, col)
        return count

    def dfs(self, grid, x, y):
        grid[x][y] = "0"
        directions = [[1,0],[-1,0],[0,1],[0,-1]]
        for dx, dy in directions:
            if 0 <= x + dx < self.m and 0 <= y + dy < self.n and grid[x+dx][y+dy] == "1":
                self.dfs(grid, x + dx, y + dy)
```

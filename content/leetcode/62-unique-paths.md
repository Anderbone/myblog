+++
date = "2021-03-25"
title = "62. Unique paths"
tags = ["dp"]
+++


A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).
The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).
How many possible unique paths are there?

Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right

- code
```py
class Solution:
    def uniquePaths(self, m, n):
        cur = [1] * n
        for _ in range(1, m):
            for j in range(1, n):
                cur[j] += cur[j-1]
        return cur[-1]

```
- code
```py
class Solution:
    def uniquePaths(self, m, n):
        dp = {(0,1):1, (1,0):1}
        for row in range(m):
            for col in range(n):
                if row == 0 or col == 0:
                    dp[(row, col)] = 1
                else:
                    dp[(row, col)] = dp[(row-1, col)] + dp[(row, col-1)]
        return dp[(m-1, n-1)]

```

- code
```py
class Solution:
    def uniquePaths(self, m, n):
        return math.factorial(m+n-2)//(math.factorial(n-1) * math.factorial(m-1))
```
- code  time limit exceeded
```py
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        if m == 1 or n == 1:
            return 1
        return self.uniquePaths(m-1, n) + self.uniquePaths(m, n-1)

```
- code
```py
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        grid = [[1 for _ in range(n)] for _ in range(m)]
        for i in range(1, m):
            for j in range(1, n):
                grid[i][j] = grid[i][j-1]+grid[i-1][j]
                    
        return grid[-1][-1]

```
- c  default reverse, same as above
```py
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        grid = [[0 for i in range(m)] for j in range(n)]
        for i in range(n):
            for j in range(m):
                if i == 0 or j == 0:
                    grid[i][j] = 1
                else:
                    grid[i][j] = grid[i][j-1]+grid[i-1][j]
                    
        return grid[n-1][m-1]
```

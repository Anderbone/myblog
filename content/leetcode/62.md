+++ 
date = "2022-01-12"
title = "62. Unique Paths"
tags = ["dp"]
+++

[Unique Paths - LeetCode](https://leetcode.com/problems/unique-paths/)

There is a robot on an m x n grid. The robot is initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time.
Given the two integers m and n, return __the number of possible unique paths that the robot can take to reach the bottom-right corner__.
The test cases are generated so that the answer will be less than or equal to 2 * 109.
 
Example 1:
![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)Input: m = 3, n = 7 Output: 28 

Example 2:
Input: m = 3, n = 2 Output: 3 Explanation: From the top-left corner, there are a total of 3 ways to reach the bottom-right corner: 1. Right -> Down -> Down 2. Down -> Down -> Right 3. Down -> Right -> Down 
 
Constraints:

	1 <= m, n <= 100

---
- code  time limit exceeded
```
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        if m == 1 or n == 1:
            return 1
        return self.uniquePaths(m-1, n) + self.uniquePaths(m, n-1)

```
- code
```
class Solution:
    def uniquePaths(self, m, n):
        dp = {}
        for row in range(m):
            for col in range(n):
                if row == 0 or col == 0:
                    dp[(row, col)] = 1
                else:
                    dp[(row, col)] = dp[(row-1, col)] + dp[(row, col-1)]
        return dp[(m-1, n-1)]

```
- code
```
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        grid = [[1 for _ in range(n)] for _ in range(m)]
        for i in range(1, m):
            for j in range(1, n):
                grid[i][j] = grid[i][j-1]+grid[i-1][j]
                    
        return grid[-1][-1]

```
- code
```
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
    def uniquePaths(self, m: int, n: int) -> int:
        if m > n: n, m = m, n

        dp = [0] * m
        dp[0] = 1 # row
        for _ in range(n):
            for row in range(1, m):
                dp[row] += dp[row - 1]
        return dp[-1]
        
        
```
- code
```
class Solution:
    def uniquePaths(self, m, n):
        return math.factorial(m+n-2)//(math.factorial(n-1) * math.factorial(m-1))
```

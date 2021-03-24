
+++
date = "2021-03-24"
title = "240. Search a 2D Matrix II"
tags = ["leetcode","searching"]
+++


[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
Given target = 5, return true.
Given target = 20, return false.

- code
```py
class Solution:
    def searchMatrix(self, matrix, target):
        for row in matrix:
            for i in reversed(range(len(row))):
                if target == row[i]: return True
                if target > row[i]: break
        return False
```
- code, start from top right 
```py
class Solution:
    def searchMatrix(self, matrix, target):
        row, col = 0, len(matrix[0]) - 1 
        while row < len(matrix) and col >= 0:
            if matrix[row][col] == target:
                return True
            elif matrix[row][col] < target:
                row += 1
            else:
                col -= 1
        return False

```
- code, start from left bottom
```py
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        for i in reversed(range(len(matrix))):
            j = 0
            if matrix[i][j] > target:
                continue
            else:
                while j < len(matrix[0]) and matrix[i][j] <= target:
                    if matrix[i][j] == target:
                        return True
                    j += 1
        return False
                    

```

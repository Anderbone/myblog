+++
date = "2021-03-07"
title = "73. Set matrix zeroes"
tags = ["leetcode","array"]
+++


Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it [in-place](https://en.wikipedia.org/wiki/In-place_algorithm).
Example 1:
Input: [   [1,1,1],   [1,0,1],   [1,1,1] ] Output: [   [1,0,1],   [0,0,0],   [1,0,1] ]

- code
```py
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        def setRowToZero(m, rows):
            for r_0 in rows:
                m[r_0] = [0] * len(m[0])
        
        def setColToZero(m, cols):
            for c_0 in cols:
                for eachRow in range(len(m)):
                    m[eachRow][c_0] = 0

        rows, cols = set(), set()
        for i in range(len(matrix)):
            for j in range(len(matrix[i])):
                if matrix[i][j] == 0:
                    rows.add(i)
                    cols.add(j)
        
        setRowToZero(matrix, rows)
        setColToZero(matrix, cols)
```
- code
```py
class Solution:
    def setZeroes(self, matrix):
        # First row has zero?
        m, n, firstRowHasZero = len(matrix), len(matrix[0]), not all(matrix[0])
        # Use first row/column as marker, scan the matrix
        for i in range(1, m):
            for j in range(n):
                if matrix[i][j] == 0:
                    matrix[0][j] = matrix[i][0] = 0
        # Set the zeros
        for i in range(1, m):
            for j in range(n - 1, -1, -1):
                if matrix[i][0] == 0 or matrix[0][j] == 0:
                    matrix[i][j] = 0
        # Set the zeros for the first row
        if firstRowHasZero:
            matrix[0] = [0] * n

```

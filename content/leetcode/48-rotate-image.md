+++
date = "2021-01-09"
title = "48. Rotate image"
tags = ["leetcode","array"]
+++

Example 1:
Given input matrix =  
[ [1,2,3],  
[4,5,6],  
[7,8,9] ],  
rotate the input matrix in-place such that it becomes:
[[7,4,1],  
[8,5,2],  
[9,6,3] ]  

- code
```   python 
def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        size = len(matrix) - 1

        for i in range(len(matrix) // 2):
            for j in range(i, size - i):
                matrix[i][j], matrix[~j][i], matrix[~i][~j],matrix[j][~i] = matrix[~j][i], matrix[~i][~j], matrix[j][~i], matrix[i][j]
```
- c  transpose then 1,4 col  exchange, 2,3 col exchange
```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        trans = [[row[i] for row in matrix] for i in range(len(matrix[0]))]
        
        for i in trans:
            for j in range(int(len(trans[0])/2)):
                i[j], i[len(trans[0])-1-j] = i[len(trans[0])-1-j], i[j]
                
        matrix[:] = trans
```

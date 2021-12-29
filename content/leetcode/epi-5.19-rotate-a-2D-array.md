+++ 
date = "2020-12-25"
title = "Rotate a 2D array"
tags = ["array"]
+++
rotate_matrix
rotate 90 degrees clockwise  
- c1 ans  , O(1) space,
`for i in len(matrix)//2` is every circle level, `for j in range(i, len(matrix)-1-i)`
e.g. n=4, outside round and inside round, so 2 rounds in total.
for each round, first need 3, second need 1.
change i and j, then add ~ to the first one.   i j, ~j i, ~i ~j, j ~i
(i,j) 1 (~j,i) 13 (~i,~j) 16 (j, ~i) 4  = (~j,i) 13 (~i,~j) 16 (j, ~i) 4  (i,j) 1
```python
def rotate_matrix(square_matrix: List[List[int]]) -> None:

    matrix_size = len(square_matrix) - 1
    for i in range(len(square_matrix) // 2):
        # print(i)
        for j in range(i, matrix_size - i):
            # Perform a 4-way exchange. Note that A[~i] for i in [0, len(A) - 1]
            # is A[-(i + 1)].
            (square_matrix[i][j], square_matrix[~j][i], square_matrix[~i][~j],
             square_matrix[j][~i]) = (square_matrix[~j][i],
                                      square_matrix[~i][~j],
                                      square_matrix[j][~i],
                                      square_matrix[i][j])
```
- c2 own brute force
```python
def rotate_matrix(square_matrix: List[List[int]]) -> None:
    width = len(square_matrix)
    new_square = []
    for i in range(width):
        last_row = square_matrix.pop(-1)
        for j, e in enumerate(last_row):
            if len(new_square) < width:
                new_square.append([e])
            else:
                new_square[j].append(e)
    square_matrix[:] = new_square
```
- c0  transpose then exchange
row 1,4 2,3
```python
def rotate_matrix(square_matrix):
    if not square_matrix:
        return []
    trans = [[row[i] for row in square_matrix] for i in range(len(square_matrix[0]))]

    for i in trans:
        for j in range(len(trans[0]) // 2):
            i[j], i[len(trans[0]) - 1 - j] = i[len(trans[0]) - 1 - j], i[j]
    square_matrix[:] = trans
```

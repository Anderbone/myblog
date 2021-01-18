+++ 
date = "2020-12-25"
title = "Compute rows in Pascal's triangle"
tags = ["epi","array"]
+++
generate_pascal_triangle  
takes a nonnegative integer n and returns the first n rows of Pascal's triangle
code
- own, recursive
  code
```python
def generate_pascal_triangle(n: int) -> List[List[int]]:
    if n == 0:
        return []
    if n == 1:
        return [[1]]

    def getNextRow(lastRow):
        nextRow = [1]
        for i in range(len(lastRow) - 1):
            nextRow.append(lastRow[i] + lastRow[i+1])
        nextRow.append(1)
        return nextRow

    last_tri = generate_pascal_triangle(n - 1)
    last_tri.append(getNextRow(last_tri[-1]))
    return last_tri
```
- c ans
  code
```python
def generate_pascal_triangle(n: int) -> List[List[int]]:

    result = [[1] * (i + 1) for i in range(n)]
    # print(result)  all 1 in the triangle
    for i in range(n):
        for j in range(1, i):
            # Sets this entry to the sum of the two above adjacent entries.
            result[i][j] = result[i - 1][j - 1] + result[i - 1][j]
    return result
```

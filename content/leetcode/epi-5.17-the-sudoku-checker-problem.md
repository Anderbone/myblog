+++ 
date = "2020-12-19"
title = "The sudoku checker problem"
tags = ["epi","array"]
+++
is_valid_sudoku
check nine row constraints, nine column constraints and nine sub-grid constraints. ensure no number in [1,9] appears more than once  
A 0-value in the 2D array indicates that entry is blank, every other entry is in [1,9]
- code
c own w
code
```python
def is_valid_sudoku(partial_assignment: List[List[int]]) -> bool:

    # TODO - you fill in here.
    def check_9num(list_9num):
        counter = collections.Counter(list_9num)
        for num in counter:
            if num != 0 and counter[num] > 1:
                return False
        return True

    for row in partial_assignment:
        if check_9num(row) is False:
            return False

    for i in range(9):
        col = list()
        for j in range(9):
            col.append(partial_assignment[j][i])
        if check_9num(col) is False:
            return False

    def cut(partial_assignment, starti, endi, startj, endj):
        small = []
        for i in partial_assignment[starti:endi]:
            small += i[startj:endj]
        return small

    for i in [[0,3],[3,6],[6,9]]:
        for j in [[0,3],[3,6],[6,9]]:
            small = cut(partial_assignment, i[0], i[1], j[0], j[1])
            if check_9num(small) is False:
                return False
    return True
```
- c ans, cleaner
3, 6, 9 can be calculated by region_size
code
```python
# Check if a partially filled matrix has any conflicts.
def is_valid_sudoku(partial_assignment: List[List[int]]) -> bool:

    # Return True if subarray
    # partial_assignment[start_row:end_row][start_col:end_col] contains any
    # duplicates in {1, 2, ..., len(partial_assignment)}; otherwise return
    # False.
    def has_duplicate(block):
        block = list(filter(lambda x: x != 0, block))
        return len(block) != len(set(block))

    n = len(partial_assignment)
    # Check row and column constraints.
    if any(
            has_duplicate([partial_assignment[i][j] for j in range(n)])
            or has_duplicate([partial_assignment[j][i] for j in range(n)])
            for i in range(n)):
        return False

    # Check region constraints.
    region_size = int(math.sqrt(n))
    return all(not has_duplicate([
        partial_assignment[a][b]
        for a in range(region_size * I, region_size * (I + 1))
        for b in range(region_size * J, region_size * (J + 1))
    ]) for I in range(region_size) for J in range(region_size))
```

+++
date = "2021-01-08"
title = "36. Valid Sudoku"
tags = ["leetcode","array"]
+++


Each row must contain the digits 1-9 without repetition.
	Each column must contain the digits 1-9 without repetition.
	Each of the 9 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.

- code  twist the ans from EPI
```python    
def isValidSudoku(self, board: List[List[str]]) -> bool:

        # Return True if subarray
        # board[start_row:end_row][start_col:end_col] contains any
        # duplicates in {1, 2, ..., len(board)}; otherwise return
        # False.
        def has_duplicate(block):
            block = list(filter(lambda x: x != '.', block))
            return len(block) != len(set(block))

        n = len(board)
        # Check row and column constraints.
        if any(
                has_duplicate([board[i][j] for j in range(n)])
                or has_duplicate([board[j][i] for j in range(n)])
                for i in range(n)):
            return False

        # Check region constraints.
        region_size = int(math.sqrt(n))
        return all(not has_duplicate([
            board[a][b]
            for a in range(region_size * I, region_size * (I + 1))
            for b in range(region_size * J, region_size * (J + 1))
        ]) for I in range(region_size) for J in range(region_size))
```
- code own
```python   
def isValidSudoku(self, board: List[List[str]]) -> bool:

        def check9num(nums):
            seen = []
            for v in nums:
                if v != '.' :
                    if v not in seen:
                        seen.append(v)
                    else:
                        return False
            return True


        if not all(list(check9num(row) for row in board)):
            return False

        for i in range(9):
            thiscol = []
            for j in range(9):
                thiscol.append(board[j][i])
            if not check9num(thiscol):
                return False

        for I in range(3):
            for J in range(3):
                little_squire = []
                for i in range(3*I, 3*(I+1)):
                    for j in range(3*J, 3*(J+1)):
                        little_squire.append(board[i][j])
                if not check9num(little_squire):
                    return False

        return True
```

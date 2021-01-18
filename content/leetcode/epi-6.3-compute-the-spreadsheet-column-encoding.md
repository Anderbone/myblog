+++ 
date = "2020-12-26"
title = "Compute the spreadsheet column encoding"
tags = ["epi","string"]
+++
converts a spreadsheet column id to the corresponding integer  
return 4 for D, 27 for AA,(26 *1 + 1) 702 for ZZ(26 *26 + 26)

- code, same logic as answer
```python
def ss_decode_col_id(col: str) -> int:
    to_num = lambda x: ord(x) - 64
    f = lambda x, y: x * 26 + y
    res = functools.reduce(f, map(to_num, col))
    return res
```
- c ans
```python
def ss_decode_col_id(col):

    return functools.reduce(
        lambda result, c: result * 26 + ord(c) - ord('A') + 1, col, 0)
```

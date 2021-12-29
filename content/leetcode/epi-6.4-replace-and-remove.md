+++ 
date = "2020-12-26"
title = "replace and remove"
tags = ["string"]
+++
Apply to an array of characters, replace 'a' by 'dd', delete each entry containing a 'b'  
E.g. (a,c,d,b,b,c,a) results in the array (d,d,c,d,c,d,d).
- code, ans
```python
def replace_and_remove(size: int, s: List[str]) -> int:

    # Forward iteration: remove 'b's and count the number of 'a's.
    write_idx, a_count = 0, 0
    for i in range(size):
        if s[i] != 'b':
            s[write_idx] = s[i]
            write_idx += 1
        if s[i] == 'a':
            a_count += 1

    # Backward iteration: replace 'a's with 'dd's starting from the end.
    cur_idx = write_idx - 1
    write_idx += a_count - 1
    final_size = write_idx + 1
    while cur_idx >= 0:
        if s[cur_idx] == 'a':
            s[write_idx - 1:write_idx + 1] = 'dd'
            write_idx -= 2
        else:
            s[write_idx] = s[cur_idx]
            write_idx -= 1
        cur_idx -= 1
    return final_size
```
c0 brute force with O (n) space
```python
def replace_and_remove(size, s):
    st = ''.join(s)
    st = st.replace('a','dd')
    st= st.replace('b','')
    s[:] = st
    return len(st)
```

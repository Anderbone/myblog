+++ 
date = "2020-12-28"
title = "Test for overlapping lists"
tags = ["linkedlist"]
+++
takes two cycle-free single linked list, determines if there exists a node that is common to both lists  
![Pasted image](https://i.imgur.com/r1u1amI.png)
- c1 
```python
def overlapping_no_cycle_lists(l0, l1):
    def length(L):
        length = 0
        while L:
            length += 1
            L = L.next
        return length

    l0_len, l1_len = length(l0), length(l1)
    if l0_len > l1_len:
        l0, l1 = l1, l0  # l1 is the longer list
    # Advances the longer list to get equal length lists.
    for _ in range(abs(l0_len - l1_len)):
        l1 = l1.next

    while l0 and l1 and l0 is not l1:
        l0, l1 = l0.next, l1.next
    return l0  # None implies there is no overlap between l0 and l1.
```

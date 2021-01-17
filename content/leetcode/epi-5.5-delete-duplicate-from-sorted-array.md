+++ 
date = "2020-12-15"
title = "delete duplicate from sorted array"
tags = ["epi","array"]
+++
delete_duplicates  

(2,3,5,5,11,11)->(2,3,5,11,0,0)
takes as input a sorted array, updates it so that all duplicates have been removed and the remaining elements have been shifted left.
return the number of valid elements. can not use library functions
thought
make a write index, to move when you write a different number
### code
- c2, same to c0, easier to understand
code
```
def delete_duplicates(A: List[int]) -> int:
    if not A:
        return 0
    write_index = 1
    for i in range(1, len(A)):
        if A[i] > A[write_index-1]:
            A[write_index] = A[i]
            write_index += 1
    return write_index
```
- c1 maybe it's cheat
code, maybe it's cheat
```
def delete_duplicates(A: List[int]) -> int:
    dic = collections.Counter(A)
    for i,v in enumerate(dic.keys()):
        A[i] = v
    return len(dic)
```
- c0 old
```
# Returns the number of valid entries after deletion.
def delete_duplicates(A):
    # TODO - you fill in here.
    if not A:
        return None
    index = 0
    for i in A:
        if i != A[index]:
            index += 1
            A[index] = i

    return index+1
```

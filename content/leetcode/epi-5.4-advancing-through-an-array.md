+++ 
date = "2020-12-15"
title = "Advancing through an array"
tags = ["array"]
+++
can_reach_end

A=[3,3,1,0,2,0,1], represent the board game
ans: take 1 step from A[0] to A[1], then 3 steps from A[1] to A[4], then 2 steps from A[4] to A[6].
Note that A[0]=3>=1, A[1]= 3 >=3, A[4]=2>=2. so valid.  
Write a program which takes an array of n integers, where A[i] denotes the maximum you can advance from index i, and returns whether it's possible to adavance to the last index starting from the beginning of the array.
code
- code1
  code
```python
def can_reach_end(A):
    if A == [0]:
        return True
    step_need = 1
    for i in reversed(range(len(A)-1)):
        if A[i] < step_need:
            step_need += 1
        else:
            step_need = 1
    if A[0] >= step_need:
        return True
    return False
```
- code2 old
  c old
```python
def can_reach_end(A):
    k = 0
    for i in range(len(A)-2, -1, -1):
        if A[i] > k:
            k = 0
        else:
            k += 1

    if k == 0:
        return True
    return False
```

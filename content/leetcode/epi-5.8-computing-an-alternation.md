+++ 
date = "2020-12-16"
title = "Computing an alternation"
tags = ["epi","array"]
+++
rearrange
1<=2>=3<=4>=5...
takes an array A of n numbers, and rearranges A's elements to get a new array B having the property that B[0] <= B[1] >= B[2] <= B[3] >= B[4] <= B[5]
19,2,45,44,23,1,9,19
2,45,19,44,1, 23, 9, 19
code
- c2, best O(n)
  notice [2,3,2], when i =2, A[i:i+2] = 2, there's no index out of array issue
  code
```python
def rearrange(A: List[int]) -> None:
    for i in range(len(A)):
        A[i:i+2] = sorted(A[i:i+2], reverse= i%2 == 1)
```
- c0, old, don't need to sort, O(n)
  c
```python
def rearrange(A):
    # TODO - you fill in here.
    for i in range(len(A)-1):
        if i%2 == 0:
            if A[i] > A[i+1]:
                A[i], A[i+1] = A[i+1], A[i]
        else:
            if A[i] < A[i+1]:
                A[i], A[i+1] = A[i+1], A[i]
    return A
```
- c1 sort, O(nlogn), worse than c0, but practically quicker..
  code
```python
def rearrange(A: List[int]) -> None:
    A.sort();
    for i in range(1, len(A)-1, 2):
        A[i], A[i+1] = A[i+1], A[i]
```

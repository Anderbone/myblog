+++ 
date = "2020-12-16"
title = "Permute the elements of an array"
tags = ["array"]
+++
apply_permutation
given an array A of elements and a premutation P, apply P to A
A abcd,  P 2013, yields **bcad**
2013 means move location 0 to 2, 1 to 0, 2 to 1, 3 to 3
code
- c0   simple but need a lot space, not in place!
  c0
```python
def apply_permutation(perm, A):
    # TODO - you fill in here.
    B = [0] * len(A)
    for i in zip(A, perm):
        B[i[1]] = i[0]
    return B
```
still copy
code
```python
def apply_permutation(perm: List[int], A: List[int]) -> None:
    index_ele = list(zip(range(len(A)), A))
    for i in range(len(perm)):
        A[perm[i]] = index_ele[i][1]
    return A
```
c1
every permutation can be represented by a collection of independent permutations, each of which is cyclic, that is, it moves all elements by a fixed offset, wrapping around.
__we move a to 2, and at the same time it means location 2 is fixed, so swap the perm index with location 2__
abcd 2013
i = 0,
cbad 1023
i = 1
bcad 0123

code
```python
def apply_permutation(perm: List[int], A: List[int]) -> None:

    for i in range(len(A)):
        while perm[i] != i:
            A[perm[i]], A[i] = A[i], A[perm[i]]
            perm[perm[i]], perm[i] = perm[i], perm[perm[i]]
```
c2 old ans, not read
c1
```python
def apply_permutation(perm, A):

    for i in range(len(A)):
        # Check if the element at index i has not been moved by checking if
        # perm[i] is nonnegative.
        next = i
        while perm[next] >= 0:
            A[i], A[perm[next]] = A[perm[next]], A[i]
            temp = perm[next]
            # Subtracts len(perm) from an entry in perm to make it negative,
            # which indicates the corresponding move has been performed.
            # perm[next] -= len(perm)
            perm[next] = -1
            next = temp
    # Restore perm.
    # perm[:] = [a + len(perm) for a in perm]
```

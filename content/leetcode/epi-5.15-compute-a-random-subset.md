+++ 
date = "2020-12-17"
title = "Compute a random subset"
tags = ["epi","array"]
+++
random_subset  
input a positive integer n and a size k<=n, return a size k subset of {0,1,2...n-1}
code
difference between this one and 5.12, is that 5.12 give A, this A = list(range(n))
- c0  451 439
```python
def random_subset(n, k):
    # TODO - you fill in here.
    A = list(range(n))
    A[:] = random.sample(A, k)
    return A
```
- c1 own 437 386
```python
def random_subset(n, k):
    A = list(range(n))

    for i in range(k):
        r = random.randrange(i, n)
        A[i], A[r] = A[r], A[i]
    # A[:] = random.sample(A, k)
    return A[:k]
```

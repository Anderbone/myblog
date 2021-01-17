+++ 
date = "2020-12-17"
title = "Sample offline data"
tags = ["epi","array"]
+++
random_sampling
takes an array of distinct elements and a size, and returns a subset of the given size. All subsets should be equally likely. Return the result in input array itself
A = 3,7,5,11  k =3, ans = 5,11,3
code
- c0
```python
def random_sampling(k, A):

    for i in range(k):
        # Generate a random index in [i, len(A) - 1].
        r = random.randint(i, len(A) - 1)
        A[i], A[r] = A[r], A[i]
```
- c1
```python
def random_sampling_pythonic(k, A):
    A[:] = random.sample(A, k)
```

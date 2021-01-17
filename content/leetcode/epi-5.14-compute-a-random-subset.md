+++ 
date = "2020-12-17"
title = "Compute a random permutation"
tags = ["epi","array"]
+++
compute_random_permutation  
n = 4,  output 1230  
create uniformly random permutations, you are given a random number generator  [5.12 !(2019-07-12)  sample offline data  1](https://dynalist.io/d/MpU_i9aOQTQsEWc_dDKqqBz2#z=PYcQv_3iN48w9tfVha3rgq_k) , use as few calls to it as possible
c, basically same question as 5.12
c
```python
def random_sampling(k, A):

    for i in range(k):
        # Generate a random index in [i, len(A) - 1].
        r = random.randint(i, len(A) - 1)
        A[i], A[r] = A[r], A[i]

def compute_random_permutation(n):

    permutation = list(range(n))
    random_sampling(n, permutation)
    return permutation
```

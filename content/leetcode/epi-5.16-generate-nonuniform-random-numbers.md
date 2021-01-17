+++ 
date = "2020-12-18"
title = "Generate nonuniform random numbers"
tags = ["epi","array"]
+++
nonuniform_rando_number_generation (values, probabilities)  
given n numbers as well as probabilities p0,p1..p(n-1), which sum up to 1. given a random number generator that produces values in [0,1) uniformly, how to generate one of the n numbers according to the specified probabilities?  
3,5,7,11 and p is 9/18, 6/18, 2/18, 1/18, then in 1000 calls to your program, 3 should appear 500 etc.
- c myown
code
```python
def nonuniform_random_number_generation(values: List[int],
                                        probabilities: List[float]) -> int:
    # TODO - you fill in here.
    probsum = list()
    p_sofar = 0
    for p in probabilities:
        p_sofar += p
        probsum.append(p_sofar)
    probsum_value_dic = dict(zip(probsum, values))
    random_p = random.random()
    for p in probsum:
        if random_p < p:
            return probsum_value_dic[p]
```
- c answer
```python
def nonuniform_random_number_generation(values, probabilities):

    prefix_sum_of_probabilities = list(itertools.accumulate(probabilities))
    interval_idx = bisect.bisect(prefix_sum_of_probabilities, random.random())
    return values[interval_idx]
```
since the p_sum array is sorted, we can use binary search to find the interval in O(logn) time

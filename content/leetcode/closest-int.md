+++ 
date = "2020-05-15"
title = "Find a closest integer with the same weight"
tags = ["leetcode","primitive","bit"]
+++

> The weight of x to be the number of bits that are set to 1 in its binary reprentations. E.g. 92 in bas-2 is $(1011100)_2$, the weight is 4. 
> 
> Take a nonnegative integer x, return a number y with the same weight of x, and their difference is as small as possible.

The main idea is to swap the two rightmost consecutive bits that differ. The time complexity is O(n), where n is the width.
### java
```java
public class ClosestIntSameWeight {
    @EpiTest(testDataFile = "closest_int_same_weight.tsv")
    public static long closestIntSameBitCount(long x) {

        for (int i = 0; i < 64; i++) {
            short end1 = (short) (x & (1<<i));
            short end2 = (short) (x & (1<<(i+1)));
            if ((end1 != end2)&&(end1 == 0 || end2 == 0)) {
                // reverse these last two numbers
                x = (1<<i) ^ x;
                x = (1<<(i+1)) ^ x;
                return x;
            }
        }
        return x;

}

```
### python
```python
def closest_int_same_bit_count(x):

    NUM_UNSIGNED_BITS = 64
    for i in range(NUM_UNSIGNED_BITS - 1):
        if (x >> i) & 1 != (x >> (i + 1)) & 1:
            x ^= (1 << i) | (1 << (i + 1))  # Swaps bit-i and bit-(i + 1).
            return x

    # Raise error if all bits of x are 0 or 1.
    raise ValueError('All bits are 0 or 1')
```
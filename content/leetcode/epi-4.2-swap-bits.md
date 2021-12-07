+++ 
date = "2020-05-10"
title = "Swap bits"
tags = ["epi","bit"]
+++

### 5.2 in EPI java, 4.2 in EPI python.
> Swap the ith and jth bit in a long number.

The 2^i in java means the parity(XOR) of 2 and i, we need to use Math.pow to calculate the power of
 number.
```java
    public static long swapBits(long x, int i, int j) {
        // Extract the ith and jth bit
        short xi = (short) ((short) (x >> i) & 1);
        short xj = (short) ((short) (x >> j) & 1);

        if (xi == xj) {
            return x;
        }

//        long swap = 2^i + 2^j;
//        long swap0 = (long) (Math.pow(2,i) + Math.pow(2, j));
        long swap0 =  ((long)Math.pow(2,i) + (long)Math.pow(2, j));
        long swap1 = (1L<<i) | (1L<<j);

        return x ^ swap0;
    }
```
The interesting part is to get the bitMask. Why is this line wrong?
```java
    long swap0 = (long) (Math.pow(2,i) + Math.pow(2, j));
```
It passes some tests, however when the i or j is big enough, e.g. i = 58, j = 2, the result = $2
^{58}$ rather than $2^{58} + 2^2$. Since the type of int and long, it's beyond the limit of $2^{32}$
 and causes overflow. We need to either explicitly cast both number to long type, or use bit shift.
 ```java
    long swap0 =  ((long)Math.pow(2,i) + (long)Math.pow(2, j));
    long swap1 = (1L<<i) | (1L<<j);
```
The time complexity is O(1).

Python version:
```python
def swap_bits(x, i, j):

    # Extract the i-th and j-th bits, and see if they differ.
    if (x >> i) & 1 != (x >> j) & 1:
        # i-th and j-th bits differ. We will swap them by flipping their values.
        # Select the bits to flip with bit_mask. Since x^1 = 0 when x = 1 and 1
        # when x = 0, we can perform the flip XOR.
        bit_mask = (1 << i) | (1 << j)
        x ^= bit_mask
    return x

```
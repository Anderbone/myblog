+++
date = "2021-03-01"
title = "191. Number of 1 bits"
tags = ["leetcode","bit"]
+++

Write a function that takes an unsigned integer and return the number of '1' bits it has (also known as the [Hamming weight](http://en.wikipedia.org/wiki/Hamming_weight)).
 
Example 1:
Input: 00000000000000000000000000001011 Output: 3 Explanation: The input binary string 00000000000000000000000000001011 has a total of three '1' bits.

- code
```py
class Solution:
    def hammingWeight(self, n: int) -> int:
        return str(bin(n)).count("1")

```
- code
```py
class Solution:
    def hammingWeight(self, n: int) -> int:
        count = 0
        while n:
            count += n & 1
            n = n >> 1
        return count

```

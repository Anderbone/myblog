+++
date = "2021-03-01"
title = "461. Hamming distance"
tags = ["bit"]
+++

The [Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance) between two integers is the number of positions at which the corresponding bits are different.
Given two integers x and y, calculate the Hamming distance.
Note:
0 ≤ x, y < 231.
Example:
Input: x = 1, y = 4 Output: 2 Explanation: 1 (0 0 0 1) 4 (0 1 0 0)

- code
```py
class Solution:
    def hammingDistance(self, x: int, y: int) -> int:
        dis = 0
        while x or y:
            dis += (x&1) ^ (y&1)
            x >>= 1
            y >>= 1
        return dis

```

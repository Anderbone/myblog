+++
date = "2021-03-01"
title = "190. Reverse bits"
tags = ["bit"]
+++
[Reverse Bits - LeetCode](https://leetcode.com/problems/reverse-bits/)2w3q1

Reverse bits of a given 32 bits unsigned integer.
 
Example 1:
Input: 00000010100101000001111010011100 Output: 00111001011110000010100101000000 Explanation: The input binary string 00000010100101000001111010011100 represents the unsigned integer 43261596, so return 964176192 which its binary representation is 00111001011110000010100101000000.

---
- code
```py
class Solution:
    def reverseBits(self, n: int) -> int:
        ret, power = 0, 31
        while n:
            ret += (n & 1) << power
            n = n >> 1
            power -= 1
        return ret
```
- code
```py
class Solution:
    def reverseBits(self, n: int) -> int:
        a = format(n,"032b")
        return int(a[::-1],2)

```

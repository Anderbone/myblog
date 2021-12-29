+++
date = "2021-03-01"
title = "190. Reverse bits"
tags = ["bit"]
+++
Reverse bits of a given 32 bits unsigned integer.
 
Example 1:
Input: 00000010100101000001111010011100 Output: 00111001011110000010100101000000 Explanation: The input binary string 00000010100101000001111010011100 represents the unsigned integer 43261596, so return 964176192 which its binary representation is 00111001011110000010100101000000.

- code
```py
class Solution:
    def reverseBits(self, n: int) -> int:
        oribin='{0:032b}'.format(n)
        reversebin=oribin[::-1]
        return int(reversebin,2)
```
- code
```py
class Solution:
    def reverseBits(self, n: int) -> int:
        a = format(n,"032b")
        return int(a[::-1],2)

```
c
```py
class Solution:
    # @param n, an integer
    # @return an integer
    def reverseBits(self, n):

        s = str(bin(n)).replace('0b','')
        s = '0'*(32-len(s)) + s
        ans = s[::-1]
        return int(ans, 2)
```

+++
date = "2021-03-30"
title = "172. Factorial Trailing Zeroes"
tags = ["math"]
+++


Given an integer n, return the number of trailing zeroes in n!.
Example 1:
Input: 3 Output: 0 Explanation: 3! = 6, no trailing zero.
Example 2:
Input: 5 Output: 1 Explanation: 5! = 120, one trailing zero.

- code
```py
class Solution:
    def trailingZeroes(self, n: int) -> int:
        res = 0
        while n >= 5:
            res += n // 5
            n //= 5
        return res

```
Zeros come from 10 which is 2*5, and 5>2, so we just need to count how many 5 this factorial has. ( Once has a 5, must has 2, must has 0)
25:  6 because 25=5*5


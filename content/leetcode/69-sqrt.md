+++
date = "2021-04-01"
title = "69. Sqrt(x)"
tags = ["leetcode","math"]
+++


Given a non-negative integer x, compute and return __the square root of__ x.
Since the return type is an integer, the decimal digits are **truncated**, and only **the integer part** of the result is returned.

- c0
```py
class Solution:
    def mySqrt(self, x: int) -> int:
        return int(x**0.5)
```
- c1
```py
class Solution:
    def mySqrt(self, x: int) -> int:
        
        left, right = 0, x
        
        while True:
            mid = left + (right-left)//2
            if mid*mid > x:
                right = mid - 1
            else:
                if (mid+1)*(mid+1) > x:
                    return mid
                left = mid + 1
```

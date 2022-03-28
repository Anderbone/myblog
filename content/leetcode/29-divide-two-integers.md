+++ 
date = "2022-03-22"
title = "29. Divide Two Integers"
tags = ["math"]
+++
[Divide Two Integers - LeetCode](https://leetcode.com/problems/divide-two-integers/)

Given two integers dividend and divisor, divide two integers without using multiplication, division and mod operator.
Return the quotient after dividing dividend by divisor.
The integer division should truncate toward zero.
Example 1:
Input: dividend = 10, divisor = 3 Output: 3

---
- c0  same idea with c1
```py
class Solution:
    def divide(self, dividend: int, divisor: int) -> int:
        a , b = dividend, divisor
        sig = (a < 0) == (b < 0)
        a, b, res = abs(a), abs(b), 0
        while a >= b:
            x = 0
            while a >= b << (x + 1): 
                x += 1
            res += 1 << x  #  res+=2**x
            a -= b << x # a -= b*(2**x)
        return min(res if sig else -res, 2**31-1)
```
- c1
```py
class Solution:
    def divide(self, dividend: int, divisor: int) -> int:
        x , y = dividend, divisor
        sig = (x < 0) == (y < 0)
        x,y = abs(x), abs(y)
        result, power = 0, 32
        y_power = y << power
        while x >= y:
            while y_power > x:
                y_power >>= 1
                power -= 1

            result += 1 << power
        # result += y_power/y
            x -= y_power
        # return result
        return min(result if sig else -result, 2**31-1)
```

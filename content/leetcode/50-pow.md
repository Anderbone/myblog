+++
date = "2021-03-31"
title = "50. Pow(x, n)"
tags = ["math"]
+++
[Pow(x, n) - LeetCode](https://leetcode.com/problems/powx-n/)


Implement [pow(x, n)](http://www.cplusplus.com/reference/valarray/pow/), which calculates x raised to the power n (xn).
Example 1:
Input: 2.00000, 10 Output: 1024.00000 
Example 2:
Input: 2.10000, 3 Output: 9.26100 
Example 3:
Input: 2.00000, -2 Output: 0.25000 Explanation: 2-2 = 1/22 = 1/4 = 0.25

- code
```py
class Solution:
    def myPow(self, x: float, n: int) -> float:
        result = 1

        if n < 0:
            n = -n
            x = 1/x

        while n:
            if n % 2 == 1:
                result *= x
            x, n = x * x, n // 2
        return result

```
- code
```py
class Solution:
    def myPow(self, x, n):
        if n < 0:
            x = 1 / x
            n = -n
        pow = 1
        while n:
            if n & 1:
                pow *= x
            x *= x
            n >>= 1
        return pow

```
- code
```py
class Solution:
    def myPow(self, x, n):
        if not n:
            return 1
        if n < 0:
            return 1 / self.myPow(x, -n)
        if n % 2:
            return x * self.myPow(x, n-1)
        return self.myPow(x*x, n/2)



```
c1
```py
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n == 0:
            return 1
        elif n == 1:
            return x

        if n < 0:
            n = abs(n)
            x = 1/x

        halfPower = self.myPow(x, n//2)
        return halfPower*halfPower*self.myPow(x, n - n//2 - n//2)
```

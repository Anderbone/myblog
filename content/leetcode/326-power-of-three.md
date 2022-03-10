+++ 
date = "2021-02-27"
title = "326. Power of Three"
tags = ["math"]
+++
[Power of Three - LeetCode](https://leetcode.com/problems/power-of-three/)

Given an integer, write a function to determine if it is a power of three.
Example 1:
Input: 27 Output: true 
Example 2:
Input: 0 Output: false

- code
```py
class Solution:
    def isPowerOfThree(self, n: int) -> bool:
        if n == 0:
            return False
        while n % 3 == 0:
            n = n / 3
        if n == 1:
            return True
        return False

```
- code, 3^20 is out of the range of Integer. 
```py
class Solution:
    def isPowerOfThree(self, n: int) -> bool:
        return n > 0 and 3**19 % n == 0

```

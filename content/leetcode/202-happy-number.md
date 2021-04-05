+++
date = "2021-03-30"
title = "202. Happy number"
tags = ["leetcode","math"]
+++

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.
Example: 
Input: 19 Output: true Explanation: 12 + 92 = 82 82 + 22 = 68 62 + 82 = 100 12 + 02 + 02 = 1

{4}
{16, 4}
{16, 4, 37}
{16, 58, 4, 37}
{4, 37, 16, 89, 58}
{4, 37, 16, 145, 89, 58}
{4, 37, 42, 16, 145, 89, 58}
{4, 37, 42, 16, 145, 20, 89, 58}  20 then 4 again..

- code
```py
class Solution(object):
    def isHappy(self, n):
        seen = set([n])
        while n != 1:
            n = sum(int(digit)**2 for digit in str(n))
            if n in seen: return False
            seen.add(n)
        return True



```
- code
```py
class Solution:
    def isHappy(self, n: int) -> bool:
        meet = set()
        while n:
            if n == 1:
                return True
            if n in meet:
                return False
            meet.add(n)
            next = 0
            while n:
                next += (n%10) ** 2
                n = n//10
            n = next
```

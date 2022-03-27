+++
date = "2021-04-01"
title = "69. Sqrt(x)"
tags = ["math"]
+++

[Sqrt(x) - LeetCode](https://leetcode.com/problems/sqrtx/)

Given a non-negative integer x, compute and return __the square root of__ x.
Since the return type is an integer, the decimal digits are **truncated**, and only **the integer part** of the result is returned.

---
- code
```java
class Solution {
  public int mySqrt(int x) {
    if (x < 2) return x;

    long num;
    int pivot, left = 2, right = x / 2;
    while (left <= right) {
      pivot = left + (right - left) / 2;
      num = (long)pivot * pivot;
      if (num > x) right = pivot - 1;
      else if (num < x) left = pivot + 1;
      else return pivot;
    }

    return right;
  }
}
```
- code
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

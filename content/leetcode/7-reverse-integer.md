+++
date = "2021-04-07"
title = "7. Reverse integer"
tags = ["leetcode","math"]
+++


Given a 32-bit signed integer, reverse digits of an integer.
Example 1:
Input: 123 Output: 321

- code
```py
class Solution(object):
    def reverse(self, x):
        s = (x > 0) - (x < 0)
        r = int(str(x*s)[::-1])
        return s*r * (r < 2**31)


```
- code
```py
class Solution:
    def reverse(self, x: int) -> int:
        if x >= 2**31-1 or x<=-2**31:
            return 0
        ans = 0
        flag = False
        num = x

        if x < 0:
            flag = True
            num = abs(x)
        while num:
            ans *= 10
            ans += num % 10
            num = num//10
            

        if flag:
            if ans*(-1)<=-2**31:
                return 0
            return ans*(-1)
        else:    
            if ans >=2**31-1:
                return 0
            return ans

```

+++
date = "2021-02-18"
title = "70. Climbing stairs"
tags = ["leetcode","dp"]
+++


You are climbing a staircase. It takes n steps to reach the top.
Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps

Example 2:
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step

The key is to realize that the solution of current number is equal to the sum of previous two solutions. The reason is that we either add one or add two each time, step[i-2] + 2 and step[i-1] + 1 are all possible solutions for step[i].
- code

- code
```py
class Solution:
    def climbStairs(self, n: int) -> int:
        cache = {1:1, 2:2}
        for i in range(3, n+1):
            cache[i] = cache[i-1] + cache[i-2]
        return cache[n]

```
- code
```py
class Solution:
    def climbStairs(self, n: int) -> int:
        dp = [0]*(n+1)
        dp[0] = 1
        for i in range(1, n+1):
            for j in [1, 2]:
                if j <= n:
                    dp[i] += dp[i-j]
        return dp[-1]

```
c2
```py
class Solution:

    def climbStairs(self, n: int) -> int:
        if  n<= 3:
            return n
        pre = 1
        cur = 2
        for i in range(n-2):
            temp = cur
            cur = pre+cur
            pre = temp
        return cur
```

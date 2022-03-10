
+++ 
date = "2021-04-08"
title = "9. Palindrome number"
tags = ["math"]
+++
[Palindrome Number - LeetCode](https://leetcode.com/problems/palindrome-number/)

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.
Example 1:
Input: 121 Output: true

- code
```py
class Solution:
    def isPalindrome(self, x: int) -> bool:
        ans = 0
        num = x
        if x < 0:
            return False
        while num:
            ans *= 10
            ans += num % 10
            num = num//10
            
        return ans == x

```
- code
```py
class Solution:
    def isPalindrome(self, x: int) -> bool:
        strx = str(x)
        return strx == strx[::-1]

```

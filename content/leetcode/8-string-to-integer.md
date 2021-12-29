+++ 
date = "2021-01-11"
title = "8. String to integer"
tags = ["string"]
+++

Input: "42"
Output: 42

Example 2:
Input: "   -42"
Output: -42
Explanation: The first non-whitespace character is '-', which is the minus sign.
Then take as many numerical digits as possible, which gets 42.

Example 3:
Input: "4193 with words"
Output: 4193

w45 return 0

- code
```python
class Solution:
    def myAtoi(self, s: str) -> int:
        purenum = []
        start_positive = False
        negative = False
        for v in s:
            if not purenum:
                if v == ' ':
                    if negative or start_positive:
                        return 0
                    continue
                elif v == "+":
                    if negative or start_positive:
                        return 0
                    start_positive = True
                    continue
                elif v == '-':
                    if start_positive or negative:
                        return 0
                    negative = True
                elif not v.isdigit():
                    return 0
            
            if v.isdigit():
                purenum.append(v)
            else:
                if purenum:
                    break

        if not purenum:
            return 0
        
        num = int("".join(purenum))
        if negative:
            return -2**31 if num > 2**31 else num * -1
        return 2**31-1 if num > 2**31-1 else num
```
- code, most votes
```python
class Solution(object):
    def myAtoi(self, s):
        """
        :type str: str
        :rtype: int
        """
        ###better to do strip before sanity check (although 8ms slower):
        #ls = list(s.strip())
        #if len(ls) == 0 : return 0
        if len(s) == 0 : return 0
        ls = list(s.strip())
        
        sign = -1 if ls[0] == '-' else 1
        if ls[0] in ['-','+'] : del ls[0]
        ret, i = 0, 0
        while i < len(ls) and ls[i].isdigit() :
            ret = ret*10 + ord(ls[i]) - ord('0')
            i += 1
        return max(-2**31, min(sign * ret,2**31-1))
```
- c RE
```python
from re import compile
class Solution:
    def myAtoi(self, s: str) -> int:
        MIN_VALUE, MAX_VALUE = - 2 ** 31, 2 ** 31 - 1
        pattern = compile(r'^ *([\+-]?\d+){1}')
        matched = pattern.match(s)
        if matched:
            return min(MAX_VALUE, max(MIN_VALUE, int(matched.group())))
        else:
            return 0
```

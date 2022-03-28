+++
date = "2021-04-01"
title = "166. Fraction to recurring decimal"
tags = ["math"]
+++
[Fraction to Recurring Decimal - LeetCode](https://leetcode.com/problems/fraction-to-recurring-decimal/)

Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.
If the fractional part is repeating, enclose the repeating part in parentheses.
Example 1:
Input: numerator = 1, denominator = 2 Output: "0.5" 
Example 2:
Input: numerator = 2, denominator = 1 Output: "2"
Example 3:
Input: numerator = 2, denominator = 3 Output: "0.(6)"

---
- code
```py
class Solution:
# @return a string
    def fractionToDecimal(self, numerator, denominator):
        n, remainder = divmod(abs(numerator), abs(denominator))
        sign = '-' if numerator*denominator < 0 else ''
        result = [sign+str(n), '.']
        stack = []
        while remainder not in stack:
            stack.append(remainder)
            n, remainder = divmod(remainder*10, abs(denominator))
            result.append(str(n))

        idx = stack.index(remainder)
        result.insert(idx+2, '(')
        result.append(')')
        return ''.join(result).replace('(0)', '').rstrip('.')

```
- c
```py
class Solution:
    def fractionToDecimal(self, numerator: int, denominator: int) -> str:
        if not numerator:
            return "0"
        sign=True if (numerator <0 and denominator <0) or (numerator >0 and denominator >0) else False
        numerator,denominator=abs(numerator),abs(denominator)
        left=str(numerator//denominator)
        numerator=numerator%denominator
        if not numerator:
            return left if sign else '-'+left
        d={}
        right=[]
        i=0
        
        while numerator:
            if numerator in d:
                right.insert(d[numerator],'(')
                right.append(')')
                break
            else:
                d[numerator]=i
                numerator*=10
                div=numerator//denominator
                right.append(str(div))
                
            numerator%=denominator
            i+=1
        return left+'.'+''.join(right) if sign else '-'+left+'.'+''.join(right)
```

+++ 
date = "2021-02-27"
title = "13. Roman to integer"
tags = ["leetcode","math"]
+++


Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.
Symbol Value I 1 V 5 X 10 L 50 C 100 D 500 M 1000
For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.
Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

 I can be placed before V (5) and X (10) to make 4 and 9. 
 X can be placed before L (50) and C (100) to make 40 and 90. 
 C can be placed before D (500) and M (1000) to make 400 and 900.Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.
Example 1:
Input: "III" Output: 3
Example 2:
Input: "IV" Output: 4

- code
```py
class Solution:
    def romanToInt(self, s: str) -> int:
        translations = {
            "I": 1,
            "V": 5,
            "X": 10,
            "L": 50,
            "C": 100,
            "D": 500,
            "M": 1000
        }
        number = 0
        s = s.replace("IV", "IIII").replace("IX", "VIIII")
        s = s.replace("XL", "XXXX").replace("XC", "LXXXX")
        s = s.replace("CD", "CCCC").replace("CM", "DCCCC")
        for char in s:
            number += translations[char]
        return number

```
- code
```py
class Solution:
    def romanToInt(self, s: str) -> int:
        if not s:
            return 0
        roman_dic = {
            "I":1,
            "V":5,
            "X":10,
            "L":50,
            "C":100,
            "D":500,
            "M":1000
        }
        res = 0
        for i in range(len(s)-1):
            if roman_dic[s[i]] < roman_dic[s[i+1]]:
                res -= roman_dic[s[i]]
            else:
                res += roman_dic[s[i]]
        res += roman_dic[s[-1]]
        return res

```

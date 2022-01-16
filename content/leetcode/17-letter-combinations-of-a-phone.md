+++ 
date = "2022-01-16"
title = " 17. Letter Combinations of a Phone Number "
tags = ["backtracking"]
+++
[Letter Combinations of a Phone Number - LeetCode](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.
A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.
![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)
 
Example 1:
Input: digits = "23" Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"] 

Example 2:
Input: digits = "" Output: [] 

Example 3:
Input: digits = "2" Output: ["a","b","c"]
---
- code
```py
class Solution(object):
    def letterCombinations(self, digits):
        if not digits: return []
        dic = {'2': "abc", '3': "def", '4': "ghi", '5': "jkl", '6': "mno", '7': "pqrs", '8': "tuv", '9': "wxyz"}

        res = []
        def backTracking(index, path):
            if index == len(digits):
                res.append("".join(path))
                return
            for c in dic[digits[index]]:
                backTracking(index + 1, path + [c])
        backTracking(0, [])
        return res

```

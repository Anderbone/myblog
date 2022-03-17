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
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits: return None
        dic = {
            "2": ["a","b","c"],
            "3": ["d","e","f"],
            "4": ["g","h","i"],
            "5": ["j","k","l"],
            "6": ["m","n","o"],
            "7": ["p","q","r","s"],
            "8": ["t","u","v"],
            "9": ["w","x","y","z"]
        }
        
        res = []
        
        def backtracking(index, path):
            if index == len(digits):
                res.append("".join(path))
                return
            for char in dic[digits[index]]:
                backtracking(index + 1, path + [char])
                
        backtracking(0, [])
        
        return res
```

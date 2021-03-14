+++
date = "2021-03-14"
title = "17. Letter combinations of a phone number"
tags = ["leetcode","backtracking"]
+++

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.  
A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].

- code
```py
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        self.dic_num = {
            "2":"abc",
            "3":"def",
            "4":"ghi",
            "5":"jkl",
            "6":"mno",
            "7":"pqrs",
            "8":"tuv",
            "9":"wxyz"
        }
        self.res = []
        self.helper(list(digits))
        return self.res


    def helper(self, nums):
        if not nums:
            return
        cur_num = nums.pop(0)
        cur_char = self.dic_num[cur_num]
        if not self.res:
            for v in cur_char:
                self.res.append(v)
        else:
            cur_list = []
            for r in self.res:
                for v in cur_char:
                    cur_list.append(r+v)
            self.res[:] = cur_list
        self.helper(nums)
        

```
- c
```py
class Solution(object):
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        def backTracking(digits, carry):
            if digits == []:
                res.append(carry)
                return

            number = digits[0]
            for j in dic[number]:
                backTracking(digits[1:], carry + j)
                 
        if not digits:
            return []
        digits = list(digits)
        res = []
        dic = {'2': "abc", '3': "def", '4': "ghi", '5': "jkl", '6': "mno", '7': "pqrs", '8': "tuv", '9': "wxyz"}
        backTracking(digits, '')
        return res

```

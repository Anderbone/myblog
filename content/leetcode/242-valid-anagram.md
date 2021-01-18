+++ 
date = "2021-01-11"
title = "242. Valid anagram"
tags = ["leetcode","string"]
+++

Given two strings s and t , write a function to determine if t is an anagram of s.
Example 1:
Input: s = "anagram", t = "nagaram" Output: true

- code
```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
        dic_s = dict(collections.Counter(s))
        dic_t = dict(collections.Counter(t))
        return dic_s == dic_t
```

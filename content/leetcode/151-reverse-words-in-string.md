+++
date = "2021-04-16"
title = "151. Reverse words in a string"
tags = ["leetcode","string"]
+++


Given an input string, reverse the string word by word.
 
Example 1:
Input: "the sky is blue" Output: "blue is sky the"

- code, [::-1] or reversed
```py
class Solution:
    def reverseWords(self, s: str) -> str:
        return " ".join(reversed(s.strip().split()))
       
```

+++
date = "2021-04-15"
title = "58. Length of last word"
tags = ["string"]
+++


Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.
If the last word does not exist, return 0.
Note: A word is defined as a character sequence consists of non-space characters only.
Example:
Input: "Hello World" Output: 5

- code
```py
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        if not s.split():
            return 0
        return len(s.split()[-1])

```
c
```py
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        if s == "" :
            return 0
        list  = s.strip().split(' ')
        return len(list[-1])
```

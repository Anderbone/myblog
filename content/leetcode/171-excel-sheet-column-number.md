+++
date = "2021-03-31"
title = "171. Excel sheet column number"
tags = ["math"]
+++


Given a column title as appear in an Excel sheet, return its corresponding column number.
For example:
 A -> 1 B -> 2 C -> 3 ... Z -> 26 AA -> 27 AB -> 28 ... 
Example 1:
Input: "A" Output: 1

- code
```py
class Solution:
    def titleToNumber(self, s: str) -> int:
        val = 0
        length = len(s)
        for i in range(length):
            val += (ord(s[i]) - ord('A') + 1) * pow(26, length - 1 - i)
        return val
```
- c0
```py
class Solution:
    def titleToNumber(self, s: str) -> int:
        num = 0
        for c in s:
            num = num * 26 + (ord(c) - ord('A') + 1)
        return num
```
- code, based on c0
```py
class Solution:
    def titleToNumber(self, s: str) -> int:
        return functools.reduce(
            lambda result, c: result * 26 + ord(c) - ord('A') + 1, s, 0
        )

```
` lambda result, c: result * 26 + ord(c) - ord('A') + 1 ` is the func
the parameter of reduce function is (func, seq, initial)

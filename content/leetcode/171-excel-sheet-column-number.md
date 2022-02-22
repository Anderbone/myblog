+++ 
date = "2022-02-22"
title = "171. Excel Sheet Column Number"
tags = ["math"]
+++
[Excel Sheet Column Number - LeetCode](https://leetcode.com/problems/excel-sheet-column-number/)

Given a string columnTitle that represents the column title as appear in an Excel sheet, return __its corresponding column number__.
For example:
A -> 1 B -> 2 C -> 3 ... Z -> 26 AA -> 27 AB -> 28 ... 
 
Example 1:
Input: columnTitle = "A" Output: 1 
Example 2:
Input: columnTitle = "AB" Output: 28 
Example 3:
Input: columnTitle = "ZY" Output: 701 
 
Constraints:

	1 <= columnTitle.length <= 7
	columnTitle consists only of uppercase English letters.
	columnTitle is in the range ["A", "FXSHRXW"].

---
- code
```py
class Solution:
    def titleToNumber(self, columnTitle: str) -> int:
        res = 0
        for c in columnTitle:
            res = (ord(c) - ord('A') + 1) + res * 26
        return res
```
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
- code
```py
class Solution:
    def titleToNumber(self, s: str) -> int:
        return functools.reduce(
            lambda result, c: result * 26 + ord(c) - ord('A') + 1, s, 0
        )

```
` lambda result, c: result * 26 + ord(c) - ord('A') + 1 ` is the func
the parameter of reduce function is (func, seq, initial)

+++ 
date = "2022-03-13"
title = "20. Valid Parentheses"
tags = ["stack"]
+++
[Valid Parentheses - LeetCode](https://leetcode.com/problems/valid-parentheses/)

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
An input string is valid if:

	Open brackets must be closed by the same type of brackets.
	Open brackets must be closed in the correct order. 
Example 1:
Input: s = "()" Output: true 
Example 2:
Input: s = "()[]{}" Output: true 
Example 3:
Input: s = "(]" Output: false 
 
Constraints:

	1 <= s.length <= 104
	s consists of parentheses only '()[]{}'

---
- code
```py
class Solution:
    def isValid(self, s: str) -> bool:
        dic = {')':'(','}':'{',']':'['}
        stack = []
        for c in s:
            if c not in dic:
                stack.append(c)
            else:
                if not stack or stack[-1] != dic[c]: return False
                stack.pop()
        return not stack
```
- code
```py
class Solution:
    def isValid(self, s: str) -> bool:
        par = {"(":")", "{":"}", "[":"]"}
        stack = []
        for v in s:
            if v in par:
                stack.append(v)
            else:
                if not stack or par[stack.pop()] != v:
                    return False
        return not stack     

```

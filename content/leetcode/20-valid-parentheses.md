+++
date = "2021-03-03"
title = "20. Valid parentheses"
tags = ["stack"]
+++

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
An input string is valid if:

	Open brackets must be closed by the same type of brackets.
	Open brackets must be closed in the correct order.

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

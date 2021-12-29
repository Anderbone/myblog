+++ 
date = "2021-04-19"
title = "205. Isomorphic strings"
tags = ["string"]
+++


Example 1:
Input: s = "egg", t = "add"Output: true 
Example 2:
Input: s = "foo", t = "bar"Output: false

- code
```py
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        return len(set(zip(s, t))) == len(set(s)) == len(set(t))
```
- code, is there a way to not check match.values? check below
```py
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        
        if len(s) != len(t):
            return False
        
        match = {}
        for i in range(len(s)):
            if s[i] not in match:
                if t[i] in match.values():
                    return False
                match[s[i]] = t[i]
            else:
                if match[s[i]] != t[i]:
                    return False
        return True


```
- code
```py
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        d= {}
        if len(set(s)) != len(set(t)): return False

        for i in range(len(s)):
            if s[i] in d and d[s[i]] != t[i]:
                return False
            else:
                d[s[i]] = t[i]
        return True

```

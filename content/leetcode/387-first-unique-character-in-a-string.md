+++ 
date = "2021-01-10"
title = "387. first unique character in a string"
tags = ["leetcode","string"]
+++

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.
Examples:
s = "leetcode" return 0. s = "loveleetcode", return 2.

- code
```py
class Solution:
    def firstUniqChar(self, s: str) -> int:
        char_count = dict(collections.Counter(s))
        for i in range(len(s)):
            if char_count[s[i]] == 1:
                return i
        return -1

```
- code
```py
def firstUniqChar(self, s: str) -> int:
        char_count = dict(collections.Counter(s))
        for char in char_count:
            if char_count[char] == 1:
                return s.index(char)
        return -1
```
- c1
```py
import string

class Solution:
    def firstUniqChar(self, s: str) -> int:
        ret = len(s)
        for c in string.ascii_lowercase:
            l, r = s.find(c), s.rfind(c)
            if l != -1 and l == r:
                ret = min(ret, l)
        return ret if ret != len(s) else -1
```

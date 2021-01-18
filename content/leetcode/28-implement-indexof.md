+++ 
date = "2020-01-13"
title = "28. Implement indexOf"
tags = ["leetcode","string"]
+++

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.
Example 1:
Input: haystack = "hello", needle = "ll" Output: 2
Example 2:
Input: haystack = "aaaaa", needle = "bba" Output: -1
return 0 if it's empty

- code best, range is the diff
```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if not needle:
            return 0
        for i in range(len(haystack) - len(needle) + 1):
            for j in range(len(needle)):
                if haystack[i+j] != needle[j]:
                    break
                if j == len(needle) - 1:
                    return i
        return -1
```
- code
```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        needle_index = 0
        if not needle:
            return 0
        if len(haystack) < len(needle):
            return -1
        for i in range(len(haystack)):
            if haystack[i] != needle[needle_index]:
                continue
            else:
                haystack_index = i
                while needle_index < len(needle) and haystack_index < len(haystack):
                    if needle[needle_index] != haystack[haystack_index]:
                        needle_index = 0
                        break
                    else:
                        if needle_index == len(needle) - 1:
                            return haystack_index - len(needle) + 1
                        needle_index += 1
                        haystack_index += 1

        return -1
```
- c
```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if needle in haystack:
            return haystack.index(needle)
        else:
            return -1
```
        

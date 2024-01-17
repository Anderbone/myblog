+++ 
date = "2024-01-17"
title = "28. Find the Index of the First Occurrence in a String"
tags = ["string"]
+++
https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/description

Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.
 
**Example 1:**
**Input:** haystack = "sadbutsad", needle = "sad" **Output:** 0 **Explanation:** "sad" occurs at index 0 and 6. The first occurrence is at index 0, so we return 0. 
**Example 2:**
**Input:** haystack = "leetcode", needle = "leeto" **Output:** -1 **Explanation:** "leeto" did not occur in "leetcode", so we return -1. 
 
**Constraints:**
 	
	1 <= haystack.length, needle.length <= 104 	
	haystack and needle consist of only lowercase English characters.

---
- code
```java
class Solution {
    public int strStr(String haystack, String needle) {
        return haystack.indexOf(needle);
    }
}
```
- code range is the diff 
```py
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
```py
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
- code
```py
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if needle in haystack:
            return haystack.index(needle)
        else:
            return -1
```
        

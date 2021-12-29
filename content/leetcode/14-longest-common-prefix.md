+++ 
date = "2021-01-14"
title = "14. Longest common prefix"
tags = ["string"]
+++

Write a function to find the longest common prefix string amongst an array of strings.
If there is no common prefix, return an empty string "".

Example 1:
Input: ["flower","flow","flight"] Output: "fl"
- zip, best ans
strs = ["flower","flow","flight"]
l = list(zip(*strs))
>>> l = [('f', 'f', 'f'), ('l', 'l', 'l'), ('o', 'o', 'i'), ('w', 'w', 'g')]
```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        l = list(zip(*strs))
        prefix = ""
        for i in l:
            if len(set(i))==1:
                prefix += i[0]
            else:
                break
        return prefix
```
- c1
  quickly once
```python
def longestCommonPrefix(self, strs: List[str]) -> str:
        if strs == []:
            return ""
        common = strs[0]
        index = len(common)
        for i in strs[1:]:
            index = min(index, len(i))
            while (common[:index] != i[:index]):
                index -= 1
        return "" if index == -1 else common[:index]
```
- c0
write so many times..
  code
```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if not strs:
            return ""
        currentShort = strs[-1]
        res = len(strs[-1])
        for i in range(len(strs)-1):
            cur = strs[i]
            # update currentShort with cur, get the common of these two
            res = min(res, len(cur))
            for j in range(res):
                if (cur[j]!=currentShort[j]):
                    res = min(res,j)
                    break
            if res==0 or cur == "":
                return ""
        return currentShort[:res]
```
- cbefore
```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if len(strs) == 0:
            return ""
        j = len(strs[0])
        for i in range(len(strs)-1):
            first = strs[i]
            second = strs[i+1]
            while (first[:j] != second[:j]):
                j  -= 1
        return strs[0][:j]
```
- thoughts  #thoughts
  if not strs: return ""
  use range is better than str[1:]

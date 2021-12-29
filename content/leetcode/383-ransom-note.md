+++
date = "2021-04-15"
title = "58. Length of last word"
tags = ["string"]
+++

Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.
Each letter in the magazine string can only be used once in your ransom note.
Note:
You may assume that both strings contain only lowercase letters.
canConstruct("a", "b") -> false canConstruct("aa", "ab") -> false canConstruct("aa", "aab") -> true

- code
```py
class Solution(object):
    def canConstruct(self, ransomNote, magazine):
        c1, c2 = collections.Counter(ransomNote), collections.Counter(magazine)
        return all(k in c2 and c2[k]>=c1[k] for k in c1)

```
- code
```py
class Solution(object):
    def canConstruct(self, ransomNote, magazine):
        return all(ransomNote.count(c)<=magazine.count(c) for c in set(ransomNote))

```

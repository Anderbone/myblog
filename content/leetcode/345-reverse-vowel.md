+++ 
date = "2021-04-17"
title = "345. Reverse vowels of a string"
tags = ["leetcode","string"]
+++


Given a string s, reverse only all the vowels in the string and return it.
The vowels are 'a', 'e', 'i', 'o', and 'u', and they can appear in both cases.

Example 1:
Input: "hello"Output: "holle"

- code
```py
class Solution:
    def reverseVowels(self, s):
        vowels = re.findall('(?i)[aeiou]', s)
        return re.sub('(?i)[aeiou]', lambda m: vowels.pop(), s)

```
- code
```py
class Solution:
    def reverseVowels(self, s: str) -> str:
        s = list(s)
        l, r = 0, len(s)-1
        while l < r:
            while s[l] not in 'aeiouAEIOU' and l < len(s)-1:
                l += 1
            while s[r] not in 'aeiouAEIOU' and r > 0:
                r -= 1
            if l < r:
                s[l], s[r] = s[r], s[l]
                l += 1
                r -= 1
        return "".join(s)

```

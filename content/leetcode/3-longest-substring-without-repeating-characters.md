+++ 
date = "2021-03-08"
title = "3. Longest substring without repeating characters"
tags = ["string"]
+++


Given a string, find the length of the longest substring without repeating characters.
Example 1:
Input: "abcabcbb"Output: 3 Explanation: The answer is "abc", with the length of 3. 
Example 2:
Input: "bbbbb"Output: 1 Explanation: The answer is "b", with the length of 1.

- code
```py
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        res = 0
        sub = []
        for i,v in enumerate(s):
            if v not in sub:
                sub.append(v)
                res = max(res, len(sub))
            else:
                cur_v_i = sub.index(v)
                sub = sub[cur_v_i+1:]
                sub.append(v)
        return res

```
c1
```py
class Solution:
    # @return an integer
    def lengthOfLongestSubstring(self, s):
        start = maxLength = 0
        usedChar = {}
        
        for i in range(len(s)):
            if s[i] in usedChar and start <= usedChar[s[i]]:
                start = usedChar[s[i]] + 1
            else:
                maxLength = max(maxLength, i - start + 1)

            usedChar[s[i]] = i

        return maxLength

```

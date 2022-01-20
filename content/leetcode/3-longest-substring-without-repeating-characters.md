+++ 
date = "2022-01-18"
title = "3. Longest Substring Without Repeating Characters"
tags = ["string"]
+++
[Longest Substring Without Repeating Characters - LeetCode](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

Given a string s, find the length of the longest substring without repeating characters.
 
Example 1:
Input: s = "abcabcbb" Output: 3 Explanation: The answer is "abc", with the length of 3. 

Example 2:
Input: s = "bbbbb" Output: 1 Explanation: The answer is "b", with the length of 1. 

Example 3:
Input: s = "pwwkew" Output: 3 Explanation: The answer is "wke", with the length of 3. Notice that the answer must be a substring, "pwke" is a subsequence and not a substring. 
 
Constraints:

	0 <= s.length <= 5 * 104
	s consists of English letters, digits, symbols and spaces.

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
- code #slidingwindow 
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

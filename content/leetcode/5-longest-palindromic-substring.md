+++ 
date = "2022-01-10"
title = "5. Longest Palindromic Substring"
tags = ["string"]
+++
[Longest Palindromic Substring - LeetCode](https://leetcode.com/problems/longest-palindromic-substring/)

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.
Example 1:
Input: "babad" Output: "bab" Note: "aba" is also a valid answer.

---
- code
```py
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        cur = s[0]
        for i in range(n):
            # odd
            l = r = i
            while 0 <= l - 1 and r + 1 < n and s[l-1] == s[r+1]:
                l -= 1
                r += 1
            if r - l + 1 > len(cur):
                cur = s[l:r+1]
                
            # even
            l = i
            r = i + 1
            if r < n and s[l] == s[r]:
                while 0 <= l - 1 and r + 1 < n and s[l-1] == s[r+1]:
                    l -= 1
                    r += 1
                if r - l + 1 > len(cur):
                    cur = s[l:r+1]
        return cur
```
- code
```py
class Solution:
    def longestPalindrome(self, s):
        self.maxlen = 0
        self.start = 0

        for i in range(len(s)):
            self.expandFromCenter(s,i,i)
            self.expandFromCenter(s,i,i+1)
        return s[self.start:self.start+self.maxlen]


    def expandFromCenter(self,s,l,r):
        while l > -1 and r < len(s) and s[l] ==s[r]:
            l -= 1
            r += 1

        if self.maxlen < r-l-1:
            self.maxlen = r-l-1
            self.start = l + 1
```
- code #slidingwindow
```py
class Solution:
    def longestPalindrome(self, s: str) -> str:
        if s == s[::-1]: return s
        
        window_len = 1
        start = 0
        for i in range(1, len(s)):
            # aaa, from index 1 to index 2, a -> aa or when aa -> aaa, increase max window by 1
            if i - window_len >= 0 and s[i - window_len:i+1] == s[i - window_len:i+1][::-1]:
                start = i - window_len
                window_len += 1
            
            # aba when coming to index 2, we find bab, from a -> bab, increase max window by 2
            elif i - window_len >= 1 and s[i - window_len - 1:i+1] == s[i - window_len - 1:i+1][::-1]:
                start = i - window_len - 1
                window_len += 2
            
        return s[start: start + window_len]
```
Maintain a max window length, for each index, we check [index - window, index] (containing index, increase the window length by 1) and [index - window -1, index] (increase window length by 2). Suppose the max window we found so far is m, for each index i, we check the substring that ends with current index, with length m+1 or m + 2, see if they are palindromic string. If so, we update start and max window length.

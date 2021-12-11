+++ 
date = "2021-03-09"
title = "5. Longest palindromic substring"
tags = ["leetcode","string"]
+++

[Longest Palindromic Substring - LeetCode](https://leetcode.com/problems/longest-palindromic-substring/)
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.
Example 1:
Input: "babad" Output: "bab" Note: "aba" is also a valid answer.

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
- c really fast. don't know..
```py
class Solution:
    def longestPalindrome(self, s):
        if s==s[::-1]:
            return s
        maxx=1 # itself
        start=0 # start point
        for i in range(1,len(s)):
            if i-maxx>=0 and s[i-maxx:i+1]==s[i-maxx:i+1][::-1]:
                start=i-maxx
                maxx+=1
                
            elif i-maxx>=1 and s[i-maxx-1:i+1]==s[i-maxx-1:i+1][::-1]:
                start=i-maxx-1
                maxx+=2
        return s[start:start+maxx]
```

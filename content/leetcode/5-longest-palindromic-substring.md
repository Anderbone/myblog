+++ 
date = "2021-03-09"
title = "5. Longest palindromic substring"
tags = ["leetcode","string"]
+++

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.
Example 1:
Input: "babad" Output: "bab" Note: "aba" is also a valid answer.

- code
```py
class Solution:
    def longestPalindrome(self, s):

        # get the longest palindrome, l, r are the middle indexes   
        # from inner to outer
        def helper(s, l, r):
            while l >= 0 and r < len(s) and s[l] == s[r]:
                l -= 1; r += 1
            return s[l+1:r]

        res = ""
        for i in range(len(s)):
            # odd case, like "aba"
            tmp = helper(s, i, i)
            if len(tmp) > len(res):
                res = tmp
            # even case, like "abba"
            tmp = helper(s, i, i+1)
            if len(tmp) > len(res):
                res = tmp
        return res

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

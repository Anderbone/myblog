+++ 
date = "2021-01-11"
title = "125. Valid Palindrome"
tags = ["string"]
+++
Example 1:
Input: "A man, a plan, a canal: Panama" Output: true  
Example 2:
Input: "race a car" Output: false  
considering only alphanumeric

- code
```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        i, j = 0, len(s)-1
        while i < j:
            while i < j and not s[i].isalnum():
                i += 1
            while i < j and not s[j].isalnum():
                j -= 1

            if s[i].lower() != s[j].lower():
                return False
            i += 1
            j -= 1
        return True
```
- c1
```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        if s == '':
            return True
        final = re.sub(r'\W+', '', s).lower()
        return final == final[::-1]
```

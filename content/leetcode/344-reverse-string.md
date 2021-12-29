+++ 
date = "2021-01-10"
title = "344. reverse string"
tags = ["string"]
+++

Write a function that reverses a string. The input string is given as an array of characters char[].
Do not allocate extra space for another array, you must do this by modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) with O(1) extra memory.
You may assume all the characters consist of [printable ascii characters](https://en.wikipedia.org/wiki/ASCII#Printable_characters).

Example 1:
Input: ["h","e","l","l","o"]Output: ["o","l","l","e","h"]

- code
```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        for i in range(len(s) // 2):
            s[i], s[~i] = s[~i], s[i]
```
- c2
```python
   l, r = 0, len(s) - 1
    while l < r : 
        # self.swap(s, l, r)
        s[l], s[r] = s[r], s[l]
        l += 1
        r -= 1
```

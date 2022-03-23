+++ 
date = "2022-03-22"
title = "283. Move Zeroes"
tags = ["array"]
+++
[Move Zeroes - LeetCode](https://leetcode.com/problems/move-zeroes/)

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.
Example:
Input: [0,1,0,3,12]Output: [1,3,12,0,0]

---
- code
```py
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        
        start = 0
        for v in nums:
            if v != 0:
                nums[start] = v
                start += 1
                
        while start < len(nums):
            nums[start] = 0
            start += 1
```
- code
```py
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        start = 0
        for i, v in enumerate(nums):
            if v != 0:
                nums[start], nums[i] = nums[i], nums[start]
                start += 1
```

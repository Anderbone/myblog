+++ 
date = "2022-02-26"
title = "169 Majority Element"
tags = ["array"]
+++
[Majority Element - LeetCode](https://leetcode.com/problems/majority-element/)

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.
You may assume that the array is non-empty and the majority element always exist in the array.
Example 1:
Input: [3,2,3] Output: 3
---
- code
```py
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        majorEle = nums[0]
        count = 1
        
        for i in range(1, len(nums)):
            if count == 0: majorEle = nums[i]
            if nums[i] == majorEle: count += 1
            else: count -= 1
            
        return majorEle       
```
- code
```py
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        return collections.Counter(nums).most_common(1)[0][0]
```
- c
```py
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        nums.sort()
        return nums[len(nums)//2]
```
        

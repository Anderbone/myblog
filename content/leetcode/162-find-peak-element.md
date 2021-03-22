+++
date = "2021-03-22"
title = "162. Find peak element"
tags = ["leetcode","searching"]
+++


A peak element is an element that is greater than its neighbors.
Given an input array nums, where nums[i] ≠ nums[i+1], find a peak element and return its index.
The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.
You may imagine that nums[-1] = nums[n] = -∞.
Example 1:
Input: nums = [1,2,3,1]Output: 2 Explanation: 3 is a peak element and your function should return the index number 2.

- code  [My clean and readable python solution - LeetCode Discuss](https://leetcode.com/problems/find-peak-element/discuss/50259)
```py
class Solution:
    def findPeakElement(self, nums):
        left = 0
        right = len(nums)-1

        while left < right:
            mid = (left+right)//2
            if nums[mid] > nums[mid+1] and nums[mid] > nums[mid-1]:
                return mid
                
            if nums[mid] < nums[mid+1]:
                left = mid+1
            else:
                right = mid-1
               
        return left



```
- code
```py
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return 0
        if nums[0] > nums[1]:
            return 0
        if nums[-1] > nums[-2]:
            return len(nums) - 1

        for i in range(1, len(nums)-1):
            if nums[i-1] < nums[i] > nums[i+1]:
                return i

```

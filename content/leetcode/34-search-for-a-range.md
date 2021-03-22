+++
date = "2021-03-22"
title = "34. Find First and Last Position of Element in Sorted Array"
tags = ["leetcode","sorting"]
+++

Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.
Your algorithm's runtime complexity must be in the order of O(log n).
If the target is not found in the array, return [-1, -1].
Example 1:
Input: nums = [5,7,7,8,8,10], target = 8 Output: [3,4]

Notice, `bisect.bisect_left(a, x, lo=0, hi = len(a))` find the first element that is __greater than or equal to__ the targeted value.  
Return the index which will keep the list sorted, if all elements in list are less than x, return index=len(A).

- code
```py
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        left_point = bisect.bisect_left(nums, target)
        if not nums or left_point == len(nums):
            return [-1,-1]
        if nums[left_point] == target:
            right_point = left_point
            while right_point+1 < len(nums) and nums[right_point+1] == target:
                right_point += 1
            return [left_point, right_point]
        else:
            return [-1,-1]
        

```

+++
date = "2021-04-13"
title = "80. Remove duplicates from sorted array II"
tags = ["leetcode","array"]
+++

Given a sorted array nums, remove the duplicates in-place such that duplicates appeared at most twice and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example 1:
Given nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively.

It doesn't matter what you leave beyond the returned length.

- code
```py
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if len(nums) < 3:
            return len(nums)
        step = 2
        for i in range(2, len(nums)):
            if nums[i] != nums[step-2]:
                nums[step] = nums[i]
                step += 1
        return step

```
- code
```py
class Solution:
    def removeDuplicates(self, nums):
        i = 0
        for n in nums:
            if i < 2 or n > nums[i-2]:
                nums[i] = n
                i += 1
        return i

```

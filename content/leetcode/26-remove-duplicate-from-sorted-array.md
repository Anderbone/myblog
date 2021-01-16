+++
date = "2021-01-03"
title = "26. Remove duplicate from sorted array"
tags = ["leetcode","array"]
+++

Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.
Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example 1:
Given nums = [1,1,2],
Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
It doesn't matter what you leave beyond the returned length.

- code
```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        if not nums:
            return 0
        i = 0
        for v in nums:
            if v != nums[i]:
                i += 1
                nums[i] = v
        return i+1
```
- c2
 ```python
def removeDuplicates2(self, nums: List[int]) -> int:
 	left = 0
 	if len(nums) == 0:
 		return 0
 	for i in range(len(nums)):
 		if nums[i] != nums[left]:
 			left+=1
 			nums[left] = nums[i]
 	return left + 1
```

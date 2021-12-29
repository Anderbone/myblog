+++
date = "2021-01-07"
title = "283. Move zeros"
tags = ["array"]
+++


Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.  
Example:
Input: [0,1,0,3,12]Output: [1,3,12,0,0]

- code, think another way, consider swap those that are not zero!
```python
index_not_zero = 0
        for i in range(len(nums)):
            if nums[i] != 0:
                nums[i], nums[index_not_zero] = nums[index_not_zero], nums[i]
                index_not_zero += 1
```
- code
```python
zero_count = i = 0
        while i < len(nums):
            if nums[i] == 0:
                nums.remove(nums[i])
                zero_count += 1
                i -= 1
            i += 1
        nums.extend([0] * zero_count)
```
It's dangerous to delete/add items in for/while loop. here after delete, need to use `i-=1` to check the next item
- c
```python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        for i in range(len(nums)-1, -1, -1):
            if nums[i] == 0:
                nums.append(nums.pop(i))
```

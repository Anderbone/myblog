+++
date = "2021-03-21"
title = "75. Sort colors"
tags = ["sorting"]
+++


Given an array nums with n objects colored red, white, or blue, sort them **[in-place](https://en.wikipedia.org/wiki/In-place_algorithm) **so that objects of the same color are adjacent, with the colors in the order red, white, and blue.
We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]

- code, when right-=1 later, need to use i <= right in the while condition
```py
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        i, left, right = 0, 0, len(nums) - 1
        while i <= right:
            if nums[i] == 0:
                nums[left], nums[i] = nums[i], nums[left]
                left += 1
                i += 1
            elif nums[i] == 2:
                nums[i], nums[right] = nums[right], nums[i]
                right -= 1
            elif nums[i] == 1:
                i += 1

```
- c , only difference is, when larger, -=1 at first. Then equal < large in while condition
```py
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        smaller, equal, larger = 0, 0, len(nums)
        while equal < larger:
            if nums[equal] == 0:
                nums[smaller], nums[equal] = 0, nums[smaller]
                equal += 1
                smaller += 1
            elif nums[equal] == 1:
                equal += 1
            else:  # ==2.
                larger -= 1
                nums[equal], nums[larger] = nums[larger], 2
```

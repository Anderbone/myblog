
+++ 
date = "2021-04-10"
title = "41. First missing positive"
tags = ["array"]
+++



Given an unsorted integer array, find the smallest missing positive integer.

Example 1:

Input: [1,2,0]
Output: 3
Example 2:

Input: [3,4,-1,1]
Output: 2

- code
```py
class Solution:
    def firstMissingPositive(self, nums):
        minMiss = 1
        num_set = set(nums)
        while True:
            if minMiss in num_set:
                minMiss += 1
            else:
                break

        return minMiss

```
- code, O(n), move each num to correct position
```py
class Solution:
    def firstMissingPositive(self, nums):
        for i in range(len(nums)):
            while 0 <= nums[i]-1 < len(nums) and nums[nums[i]-1] != nums[i]:
                tmp = nums[i]-1
                nums[i], nums[tmp] = nums[tmp], nums[i]
        for i in range(len(nums)):
            if nums[i] != i+1:
                return i+1
        return len(nums)+1



```

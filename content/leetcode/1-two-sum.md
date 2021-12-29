+++
date = "2021-01-08"
title = "01. Two sum"
tags = ["array"]
+++

Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
Given nums = [2, 7, 11, 15], target = 9, Because nums[0] + nums[1] = 2 + 7 = 9, return [0, 1].

- code
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        need_values = {}
        for i, v in enumerate(nums):
            need_value = target - v
            if need_value in need_values:
                return [need_values[need_value], i]
            else:
                need_values[v] = i
```



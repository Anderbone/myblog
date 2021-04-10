
+++ 
date = "2021-04-10"
title = "41. First missing positive"
tags = ["leetcode","array"]
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
    def firstMissingPositive(self, nums: List[int]) -> int:
        if not nums:
            return 1
        length = len(nums)
        potential_result_list = list(range(1, length+1))
        for v in nums:
            if 0 < v <= length:
                potential_result_list = list(filter(lambda a: a != v, potential_result_list))
                # potential_result_list.remove(v) 
        
        if not potential_result_list:
            return length+1
        return potential_result_list[0]

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
c0
```py
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
            i = 1
            while True:
                if i not in nums:
                    return i
                i += 1
```

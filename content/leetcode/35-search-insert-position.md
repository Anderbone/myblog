+++
date = "2021-04-14"
title = "35. Search insert position"
tags = ["leetcode","array"]
+++


Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.
You may assume no duplicates in the array.
Example 1:
Input: [1,3,5,6], 5 Output: 2

- c
```py
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        for i,v in enumerate(nums):
            if target <= v:
                return i
        return i +1
```
- code
```py
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        return bisect.bisect_left(nums, target)

```

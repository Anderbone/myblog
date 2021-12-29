+++
date = "2021-03-03"
title = "268. Missing number"
tags = ["math"]
+++

Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.
Example 1:
Input: [3,0,1] Output: 2

- code
```py
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        leng = len(nums)
        return leng * (leng+1) // 2 - sum(nums)

```

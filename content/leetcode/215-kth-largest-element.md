+++
date = "2021-03-22"
title = "215. Kth largest element in an array"
tags = ["leetcode","searching"]
+++

Given an integer array nums and an integer k, return __the__ kth __largest element in the array__.
Note that it is the kth largest element in the sorted order, not the kth distinct element.

Input: [3,2,1,5,6,4] and k = 2
Output: 5

- code
```py
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        return heapq.nlargest(k, nums)[-1]
```
- c
```py
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        nums.sort()
        return nums[-k]
```
        

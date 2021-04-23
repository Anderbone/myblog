+++ 
date = "2021-04-23"
title = "977. Squares of a sorted array"
tags = ["leetcode","array"]
+++

Given an integer array nums sorted in **non-decreasing** order, return __an array of **the squares of each number** sorted in non-decreasing order__.
 
**Example 1:**
Input: nums = [-4,-1,0,3,10] Output: [0,1,9,16,100] Explanation: After squaring, the array becomes [16,1,0,9,100]. After sorting, it becomes [0,1,9,16,100].

- code
```py
class Solution:
    def sortedSquares(self, A: List[int]) -> List[int]:
        for i in range(len(A)):
            A[i] *= A[i]
        A.sort()
        return A
```
- code
```py
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        l, r = 0, len(nums)-1
        res = collections.deque()
        while l <= r:
            if abs(nums[l]) <= abs(nums[r]):
                res.appendleft(nums[r] ** 2)
                r -= 1
            else:
                res.appendleft(nums[l] ** 2)
                l += 1

        return res



```

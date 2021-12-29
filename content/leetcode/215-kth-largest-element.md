+++
date = "2021-03-22"
title = "215. Kth largest element in an array"
tags = ["searching","binarysearch"]
+++
[Kth Largest Element in an Array - LeetCode](https://leetcode.com/problems/kth-largest-element-in-an-array/)
Given an integer array nums and an integer k, return __the__ kth __largest element in the array__.
Note that it is the kth largest element in the sorted order, not the kth distinct element.

Input: [3,2,1,5,6,4] and k = 2
Output: 5

- code
```py
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        def partition(l, r, p):
            nums[p], nums[r] = nums[r], nums[p]
            for i in range(l, r):
                if nums[i] < nums[r]:
                    nums[i], nums[l] = nums[l], nums[i]
                    l += 1
            nums[r], nums[l] = nums[l], nums[r]
            return l # p index after sorting
        
        k = len(nums) - k # kth smallest
        start, end = 0, len(nums) - 1
        while True:
            p = randint(start, end)
            p = partition(start, end, p)
            if p < k:
                start = p + 1
            elif p > k:
                end = p - 1
            else:
                return nums[p]
```
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
        

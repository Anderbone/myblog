+++ 
date = "2022-01-02"
title = "300. Longest Increasing Subsequence"
tags = ["dp","binarysearch"]
+++


Given an unsorted array of integers, find the length of longest increasing subsequence. A **subsequence** is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, [3,6,2,7] is a subsequence of the array [0,3,1,6,2,2,7].

Example:
Input: [10,9,2,5,3,7,101,18] Output: 4 Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 

---
- code dp
```py
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        dp = [1] * len(nums)
        for i in range(1, len(nums)):
            for j in range(i):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i], dp[j] + 1)

        return max(dp)
```
- code
```py
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        sq = [nums[0]]
        for i in range(1, len(nums)):
            if nums[i] > sq[-1]:
                sq.append(nums[i])
            else:
                for index in range(len(sq)):
                    if nums[i] == sq[index]: break
                    if nums[i] < sq[index]:
                        sq[index] = nums[i]
                        break
        return len(sq)
```
subsequence is always related to find and exchange the one in order.
- code #binarySearch 
```py
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        sub = []
        for num in nums:
            i = bisect_left(sub, num)
            

            # If num is greater than any element in sub
            if i == len(sub):
                sub.append(num)
            
            # Otherwise, replace the first element in sub greater than or equal to num
            else:
                sub[i] = num
        
        return len(sub)
            
```

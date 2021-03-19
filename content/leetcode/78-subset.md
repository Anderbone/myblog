+++
date = "2021-03-19"
title = "78. Subset"
tags = ["leetcode","backtracking"]
+++
Given a set of distinct integers, nums, return all possible subsets (the power set).
Note: The solution set must not contain duplicate subsets.
Example:
Input: nums = [1,2,3] Output: [ [3],   [1],   [2],   [1,2,3],   [1,3],   [2,3],   [1,2],   [] ]

- code
```py
class Solution(object):
    def subsets(self, nums):
        ret = []
        self.dfs(nums, [], ret)
        return ret
    
    def dfs(self, nums, path, ret):
        ret.append(path)
        for i in range(len(nums)):
            self.dfs(nums[i+1:], path+[nums[i]], ret)
```
- code
```py
class Solution:
    def subsets(self, nums):
        res = [[]]
        for num in nums:
            res += [item+[num] for item in res]
        return res
```

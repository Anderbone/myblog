+++ 
date = "2022-01-18"
title = "78. subsets"
tags = ["backtracking"]
+++
[Subsets - LeetCode](https://leetcode.com/problems/subsets/)

Given a set of distinct integers, nums, return all possible subsets (the power set).
Note: The solution set must not contain duplicate subsets.
Example:
Input: nums = [1,2,3] Output: [ [3],   [1],   [2],   [1,2,3],   [1,3],   [2,3],   [1,2],   [] ]
---
- code1
```py
class Solution:
    def subsets(self, nums):
        res = [[]]
        for num in nums:
            last = copy.deepcopy(res)
            for sublist in res:
                sublist.append(num)
            res += last

        return res

```
- code2 shorter version of code1
```py
class Solution:
    def subsets(self, nums):
        res = [[]]
        for num in nums:
            res += [item+[num] for item in res]
        return res
```
- code backtracking
```py
class Solution:
    def subsets(self, nums):
        res = []
        def dfs(nums, path):
            res.append(path)
            for i,v in enumerate(nums):
                # dfs(nums[:i]+nums[i+1:], res, path+[v]) has duplicate
                dfs(nums[i+1:], path+[v])
        dfs(nums, [])
        return res

```
- code backtracking, better to use index
```py
class Solution:
    def subsets(self, nums):
        res = []
        n = len(nums)
        def dfs(index, path):
            res.append(path)
            for i in range(index, n):
                dfs(i + 1, path+[nums[i]])
        dfs(0, [])
        return res
```

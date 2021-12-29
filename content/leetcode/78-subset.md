+++
date = "2021-03-19"
title = "78. Subset"
tags = ["backtracking"]
+++
Given a set of distinct integers, nums, return all possible subsets (the power set).
Note: The solution set must not contain duplicate subsets.
Example:
Input: nums = [1,2,3] Output: [ [3],   [1],   [2],   [1,2,3],   [1,3],   [2,3],   [1,2],   [] ]

- code
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

- code
```py
class Solution:
    def subsets(self, nums):
        res = []
        def dfs(nums, path, res):
            res.append(path)
            for i,v in enumerate(nums):
                # dfs(nums[:i]+nums[i+1:], res, path+[v]) has duplicate
                dfs(nums[i+1:], path+[v], res)
        dfs(nums, [], res)
        return res

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

+++
date = "2021-03-25"
title = "55. Jump game"
tags = ["dp"]
+++

Given an array of non-negative integers, you are initially positioned at the first index of the array.
Each element in the array represents your maximum jump length at that position.
Determine if you are able to reach the last index.
Example 1:
Input: [2,3,1,1,4] Output: true Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index. 
Example 2:
Input: [3,2,1,0,4] Output: false Explanation: You will always arrive at index 3 no matter what. Its maximum   jump length is 0, which makes it impossible to reach the last index.

- code
```py
class Solution:
   def canJump(self, nums: List[int]) -> bool:
        need = 1
        for i in reversed(range(len(nums)-1)):
            need = need + 1 if nums[i] < need else 1
        return need == 1

```

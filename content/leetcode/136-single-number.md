+++
date = "2021-01-05"
title = "136. Single Number"
tags = ["leetcode","array"]
+++
Given a non-empty array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?  
Example 1:
Input: [2,2,1] Output: 1

- code new way found online, with O(n) and no extra space
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        for i in range(1, len(nums)):
            nums[0] = nums[0] ^ nums[i]
        return nums[0]
```
- c2
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        dic = dict(collections.Counter(nums))
        for i in dic:
            if dic[i] == 1:
                return i
```


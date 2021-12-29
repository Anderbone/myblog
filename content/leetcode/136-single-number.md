+++
date = "2021-01-05"
title = "136. Single Number"
tags = ["array"]
+++

Given a non-empty array of integers, every element appears twice except for one. Find that single one.
Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
Example 1:
Input: [2,2,1] Output: 1

- code  with O(n) and no extra space
```py
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        for i in range(1, len(nums)):
            nums[0] = nums[0] ^ nums[i]
        return nums[0]
```
- code
```py
def singleNumber3(self, nums):
    return 2*sum(set(nums))-sum(nums)
```
- code
```py
def singleNumber4(self, nums):
    return reduce(lambda x, y: x ^ y, nums)
```
- c
```py
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        dic = dict(collections.Counter(nums))
        for i in dic:
            if dic[i] == 1:
                return i
```


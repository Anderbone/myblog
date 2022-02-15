+++ 
date = "2022-02-15"
title = "136. Single Number"
tags = ["array"]
+++
[Single Number - LeetCode](https://leetcode.com/problems/single-number/)

Given a non-empty array of integers nums, every element appears __twice__ except for one. Find that single one.
You must implement a solution with a linear runtime complexity and use only constant extra space.
 
Example 1:
Input: nums = [2,2,1] Output: 1 
Example 2:
Input: nums = [4,1,2,1,2] Output: 4 
Example 3:
Input: nums = [1] Output: 1 
 
Constraints:

	1 <= nums.length <= 3 * 104
	-3 * 104 <= nums[i] <= 3 * 104
	Each element in the array appears twice except for one element which appears only once.

---
- code
```py
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        res = 0
        for n in nums:
            res ^= n
        return res
```
- code
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

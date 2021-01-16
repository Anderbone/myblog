+++
date = "2021-01-05"
title = "217. Contains duplicate"
tags = ["leetcode","array"]
+++

Input: [1,2,3,1]
Output: true  
Input: [1,2,3,4]
Output: false  
return True if contains duplicate

- c0, it's O(n) to make a set from a list. Set result is out of order!
```python
return True if len(nums) != len(set(nums)) else False
```
- c1
```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        if not len(nums):
            return False
        nums.sort()
        left = nums[0]
        for i in nums[1:]:
            if i == left:
                return True
            left = i
        return False
``` 

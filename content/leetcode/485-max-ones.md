+++ 
date = "2021-04-21"
title = "485. Max consecutive ones"
tags = ["array"]
+++


Given a binary array nums, return __the maximum number of consecutive __1__'s in the array__.
 
**Example 1:**
Input: nums = [1,1,0,1,1,1] Output: 3 Explanation: The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.

- code
```py
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        max1 = 0
        temp1 = 0
        for v in nums:
            if v == 1:
                temp1 += 1
                max1 = max(max1, temp1)
            else:
                temp1 = 0
        return max1
```
- code better
```py
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        max1 = 0
        temp1 = 0
        for v in nums:
            if v == 1:
                temp1 += 1
            else:
                max1 = max(max1, temp1)
                temp1 = 0
        return max(max1, temp1)
```
- code
```py
class Solution:
    def findMaxConsecutiveOnes(self, nums):
        return max(map(len, ''.join(map(str, nums)).split('0')))
```



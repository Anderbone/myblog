+++
date = "2021-04-12"
title = "27. Remove elements"
tags = ["leetcode","array"]
+++
 
Given an array nums and a value val, remove all instances of that value in-place and return the new length.
Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example 1:
Given nums = [3,2,2,3], val = 3,
Your function should return length = 2, with the first two elements of nums being 2.
It doesn't matter what you leave beyond the returned length.

- code
```py
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        step = 0
        for v in nums:
            if v != val:
                nums[step] = v
                step += 1
        return step

```
- c2
 ```py
def removeElement(self, nums: List[int], val: int) -> int:
	 while (1):
		 try:
			 nums.remove(val)
		 except:
			 return len (nums)
```

+++
date = "2021-01-04"
title = "189. Rotate array"
tags = ["array"]
+++

Given an array, rotate the array to the right by k steps, where k is non-negative.

Example 1:

Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]

- code, quickest and best
```python
k = k % len(nums)
# use -k or use len(nums)-k, can't use both in a same line.
nums[:] = nums[-k:] + nums[:-k]
```
- code, slow, only 1 space
```python
k = k % len(nums)
for _ in range(k):
    nums.insert(0,nums.pop())
```
- c2, either use -k or use n-k, don't use both like n[-k:] + n[:n-k], will get [1,1] when [1]
```python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        k = k%n
        head = n - k
        nums[:] = nums[head:] + nums[:head]
```

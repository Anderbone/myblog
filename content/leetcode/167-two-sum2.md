
+++ 
date = "2021-04-08"
title = "167. Two sum II"
tags = ["leetcode","array"]
+++

Given an array of integers numbers that is already **__sorted in ascending order__**, find two numbers such that they add up to a specific target number.
Return the indices of the two numbers (**1-indexed**) as an integer array answer of size 2, where 1 <= answer[0] < answer[1] <= numbers.length.
You may assume that each input would have **exactly one solution** and you **may not** use the same element twice.

- code
```py
class Solution:
    def twoSum(self, numbers, target):
        left = 0
        right = len(numbers) - 1
        while numbers[left] + numbers[right] != target and left < right:
            Sum = numbers[left] + numbers[right]
            if Sum > target:
                right = right - 1
            else:
                left = left + 1
        if left < right:
            return [left + 1, right + 1]
        return []

```
- c0
```py
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        
        dic = {}
        
        for i in range(len(numbers)):
            if numbers[i] in dic:
                return [dic[numbers[i]] + 1, i + 1]
            else:
                dic[target - numbers[i]] = i
``` 


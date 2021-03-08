+++ 
date = "2021-03-08"
title = "334. Increasing triplet subsequence"
tags = ["leetcode","string"]
+++

Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.
Formally the function should:
Return true if there exists i, j, k such that arr[i] < arr[j] < arr[k] given 0 ≤ i < j < k ≤ n-1 else return false.Note: Your algorithm should run in O(n) time complexity and O(1) space complexity.

- code, use dict, logic is clearer
```py
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        temp3 = {}
        for v in nums:
            if not temp3 or v < temp3[0]:
                temp3[0] = v
            elif len(temp3) == 1 and v > temp3[0] or len(temp3) == 2 and v > temp3[0] and v < temp3[1]:
                temp3[1] = v
            elif len(temp3) == 2 and v > temp3[1]:
                return True

        return False

```
- c  list, a bit quicker
```py
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        seq = []
        
        for num in nums:
            if not seq or num > seq[-1]:
                seq.append(num)
                if len(seq) == 3:
                    return True
            elif num <= seq[0]:
                seq[0] = num
            elif num <= seq[1]:
                seq[1] = num      

        return False
```

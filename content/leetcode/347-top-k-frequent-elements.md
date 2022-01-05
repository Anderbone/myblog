+++ 
date = "2022-01-03"
title = "347. Top K Frequent Elements"
tags = ["heap"]
+++
[Top K Frequent Elements - LeetCode](https://leetcode.com/problems/top-k-frequent-elements/)

Given a non-empty array of integers, return the k most frequent elements.
Example 1:
Input: nums = [1,1,1,2,2,3], k = 2  Output: [1,2]

---
- code #quickSelection  move smaller to left
```py
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        counter = Counter(nums) # num, freq
        uniq = [k for k in counter.keys()]
        
        def partition(left, right):
            index = randint(left, right)
            freq_p = counter[uniq[index]]
            uniq[index], uniq[right] = uniq[right], uniq[index] # move pivot to the end
            for i in range(left, right):
                if counter[uniq[i]] < freq_p:
                    uniq[i], uniq[left] = uniq[left], uniq[i]
                    left += 1
            uniq[left], uniq[right] = uniq[right], uniq[left]
            return left
                    
        
        left, right = 0, len(uniq) - 1
        while left <= right:
            p = partition(left, right)
            if p == len(uniq) - k or left == right:
                return uniq[len(uniq) - k:]
                
            elif p > len(uniq) - k: # go left
                right = p - 1
            elif p < len(uniq) - k: # go right
                left = p + 1

```
- code #quickSelection  move bigger to left
```py
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        counter = Counter(nums) # num, freq
        uniq = list(counter.keys())
        
        def partition(left, right):
            for i in range(left, right): # right as pivot
                if counter[uniq[i]] > counter[uniq[right]]: # move bigger to the left
                    uniq[i], uniq[left] = uniq[left], uniq[i]
                    left += 1
            uniq[left], uniq[right] = uniq[right], uniq[left] # move pivot back to correct position
            return left
                    
        left, right = 0, len(uniq) - 1
        while left <= right:
            p = partition(left, right)
            if p == k or left == right:
                return uniq[:k]
            elif p > k: # go left
                right = p - 1
            elif p < k: # go right
                left = p + 1

```
- code   check k and length at first, so no need for left == right
```py
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        counter = Counter(nums) # num, freq
        uniq = list(counter.keys())
        if k == len(uniq): return uniq
        
        def partition(left, right):
            for i in range(left, right): # right as pivot
                if counter[uniq[i]] > counter[uniq[right]]: # move bigger to the left
                    uniq[i], uniq[left] = uniq[left], uniq[i]
                    left += 1
            uniq[left], uniq[right] = uniq[right], uniq[left] # move pivot back to correct position
            return left
                    
        left, right = 0, len(uniq) - 1
        while left <= right:
            p = partition(left, right)
            if p == k:
                return uniq[:k]
            elif p > k: # go left
                right = p - 1
            elif p < k: # go right
                left = p + 1


```
- code
```py
from collections import Counter
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]: 
        # O(1) time 
        if k == len(nums):
            return nums
        
        # 1. build hash map : character and how often it appears
        # O(N) time
        count = Counter(nums)   
        # 2-3. build heap of top k frequent elements and
        # convert it into an output array
        # O(N log k) time
        return heapq.nlargest(k, count.keys(), key=count.get) 
```
- code
```py
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = collections.Counter(nums)
        return [i[0] for i in count.most_common(k)]

```

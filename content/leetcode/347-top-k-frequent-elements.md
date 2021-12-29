+++
date = "2021-03-22"
title = "347. Top K frequent elements"
tags = ["searching"]
+++

Given a non-empty array of integers, return the k most frequent elements.
Example 1:
Input: nums = [1,1,1,2,2,3], k = 2  Output: [1,2]

- code
```py
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = collections.Counter(nums)
        return [i[0] for i in count.most_common(k)]

```
- c2
```py
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        # create dict to store the frequncy of the num appearence
        memo = {}
        for elem in nums:
            if elem in memo:
                memo[elem] += 1
            else:
                memo[elem] = 1

        # sort based on the dict value
        sorted_nums = sorted(memo.items(), key=lambda x: x[1], reverse=True)
        
        return [sorted_nums[i][0] for i in range(k)]
``` 

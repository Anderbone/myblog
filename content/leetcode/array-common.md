+++ 
date = "2020-08-22"
title = "Leetcode: Array-related commonly used functions in Python"
tags = ["leetcode", "array"]
+++

Commonly used: len(array), zip(alist,blist), enumerate(array), range(0,len(list)-1,2), collections.defaultdict(int), nums.append(val), nums.remove(val), nums.sort(), nums.reverse(), nums[:], nums.extend(nums2), min(a,b), dict(collections.Counter(nums1)), 


### e.g.1 with zip, enumerate

134 !(2019-05-28) Gas station  2  #array #2lee 

> There are N gas stations along a circular route, where the amount of gas at station i is gas[i].
> You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.
> Return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1.

Note:
If there exists a solution, it is guaranteed to be unique.
Both input arrays are non-empty and have the same length.
Each element in the input arrays is a non-negative integer.

Example 1:

Input: 
gas = [1,2,3,4,5]
cost = [3,4,5,1,2]
Output: 3

Explanation:
Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 4. Your tank = 4 - 1 + 5 = 8
Travel to station 0. Your tank = 8 - 2 + 1 = 7
Travel to station 1. Your tank = 7 - 3 + 2 = 6
Travel to station 2. Your tank = 6 - 4 + 3 = 5
Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3.
Therefore, return 3 as the starting index.

code
```python
 def canCompleteCircuit2(self, gas: List[int], cost: List[int]) -> int:
 	tmp = [x - y for x, y in zip(gas, cost)]
 	print(tmp+tmp)
 	cur = 0
 	ans = 0
 	for i, val in enumerate(tmp + tmp):
 		cur += val
 		if cur < 0:
 			ans = i + 1
			 if ans >= len(gas):
 				return -1
			 cur = 0
 	return ans
```


### e.g.2 with dict(collection.Counter(array))


> Given a non-empty array of integers, every element appears twice except for one. Find that single one.
Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
Example 1:
Input: [2,2,1] Output: 1

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        dic = dict(collections.Counter(nums))
        for i in dic:
            if dic[i] == 1:
                return i
```

+++
date = "2020-11-27"
title = "134. Gas station"
tags = ["array"]
+++

There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1.

Note:

If there exists a solution, it is guaranteed to be unique.
Both input arrays are non-empty and have the same length.
Each element in the input arrays is a non-negative integer.

> Example 1:
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
- code my own first try.
time limit exceeded, need to check index + 1, but if you use two for loop...

```python
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        diff = list(i - j for i,j in zip(gas, cost)) * 2
        # print(diff)
        for i,v in enumerate(diff):
            if v < 0:
                continue
            if i >= len(gas):
                break
            res = v
            # print("this i",i)

            for index, j in enumerate(diff[i+1:]):
                # print(res)
                res += j
                if res < 0:
                    # need to check index + 1 now.
                    break
                # if j == diff[-1]:
                if index == len(diff[i+1:]) - 1:
                    # print(i)
                    return i
        return -1
```
better ans:
```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        diff = list(i - j for i,j in zip(gas, cost)) * 2
        ans = cur = 0
        for i,v in enumerate(diff):
            cur += v
            if cur < 0:
                ans = i + 1
                cur = 0
                if i >= len(gas):
                    return -1
        return ans
```
- mistake
    - ` diff = list(i - j for i,j in zip(gas, cost)) * 2`
not for i in gas for j in ...
    - check if the last element in array,  `j==diff[-1] ` can be wrong, need to use index
    - jump to another angle to think about condition, from doing nothing to do something (change 'if ... continue' to do all things here)

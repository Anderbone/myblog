+++
date = "2021-02-20"
title = "198. House robber"
tags = ["leetcode","dp"]
+++


You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.
Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.
Example 1:
Input: [1,2,3,1] Output: 4 Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).   Total amount you can rob = 1 + 3 = 4.

Thoughts: a key to solve is to break the problem into **subproblems** such that
1. the original problem can be solved relatively easily once solutions to the subproblems are available
2. these subproblem solutions are **cached**,  caching the results of intermediate computations

For this one, it's similar to [70. Climbing stairs](https://yanjiyu.com/leetcode/70-climbing-stairs/), we need to think if we know the result(max profit) of n-1 house, given current value, is it possible to get the result of n house, what's the relationship? Looks like we can't resolve it, then what about we also have the max profit of n-2 house. Here's the relationship:
`profit[i] = max(profit[i-2]+nums[i], profit[i-1])`.

- code my own last time
```py
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums:
            return 0
        if len(nums) == 1:
            return nums[0]
        profit = {0: nums[0], 1: max(nums[0], nums[1])}
        for i in range(2, len(nums)):
            profit[i] = max(profit[i-2]+nums[i], profit[i-1])
        return profit[len(nums)-1]

```
- code  [Python DP solution, 4 line, O(n) time, O(1) space, easy to understand with detailed explanation - LeetCode Discuss](https://leetcode.com/problems/house-robber/discuss/55977)
```py
class Solution:
    # @param num, a list of integer
    # @return an integer
    def rob(self, num):
        max_3_house_before, max_2_house_before, adjacent = 0, 0, 0
        for cur in num:
            max_3_house_before, max_2_house_before, adjacent = \
            max_2_house_before, adjacent, max(max_3_house_before+cur, max_2_house_before+cur)
        return max(max_2_house_before, adjacent)

```
c0, similar to dic
```py
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return nums[0]
        dp = len(nums) * [0]
        dp[0] = nums[0]
        dp[1] = max(nums[1], nums[0])
        for i in range(2, len(nums)):
            dp[i] = max(dp[i-2] + nums[i], dp[i-1])
        return dp[-1]

```
c1
```py
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums:
            return 0
        if len(nums) < 3:
            return max(nums)
        
        pre = 0
        # a = nums[0]
        cur = nums[0]
        
        for i in range(1, len(nums)):
            temp = cur
            cur = max(nums[i]+pre,cur)
            pre = temp
        return cur
```

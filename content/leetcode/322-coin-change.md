+++ 
date = "2022-01-28"
title = "322.  Coin Change"
tags = ["dp","bfs"]
+++
[Coin Change - LeetCode](https://leetcode.com/problems/coin-change/)

You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.
Return __the fewest number of coins that you need to make up that amount__. If that amount of money cannot be made up by any combination of the coins, return -1.
You may assume that you have an infinite number of each kind of coin.
 
Example 1:
Input: coins = [1,2,5], amount = 11 Output: 3 Explanation: 11 = 5 + 5 + 1 

Example 2:
Input: coins = [2], amount = 3 Output: -1 

Example 3:
Input: coins = [1], amount = 0 Output: 0 
 
Constraints:

	1 <= coins.length <= 12
	1 <= coins[i] <= 231 - 1
	0 <= amount <= 104

---
- code bfs
```py
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        if amount == 0: return 0
        visited = set(coins)
        q = deque(coins)
        step = 1 # initial 1 coin
        while q:
            for _ in range(len(q)):
                cur = q.popleft()
                if cur == amount:
                    return step
                for c in coins:
                    nex = c + cur
                    if nex not in visited:
                        q.append(nex)
                        visited.add(nex)
            step += 1
            if all(p > amount for p in q): return -1
```
- code dp
```py
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [inf] * (amount + 1)
        dp[0] = 0
        
        for coin in coins:
            for i in range(coin, amount + 1):
                dp[i] = min(dp[i], dp[i - coin] + 1)
        return dp[-1] if dp[-1] != inf else -1 
```
 F(S)=F(S−C)+1, S is the amount, C is the denomination(value of each coin)

[1,2,5], 11
1 [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]  
2 [0, 1, 1, 2, 2, 3, 3, 4, 4, 5, 5, 6]  
5 [0, 1, 1, 2, 2, 1, 2, 2, 3, 3, 2, 3]  

5 [0, inf, inf, inf, inf, 1, inf, inf, inf, inf, 2, inf]  
2 [0, inf, 1, inf, 2, 1, 3, 2, 4, 3, 2, 4]  
1 [0, 1, 1, 2, 2, 1, 2, 2, 3, 3, 2, 3]  

![top down](https://i.imgur.com/Sl4yAkG.png)

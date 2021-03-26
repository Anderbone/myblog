+++
date = "2021-03-26"
title = "322. Coin change"
tags = ["leetcode","dp","bfs"]
+++


You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.
You may assume that you have an infinite number of each kind of coin.

Example 1:
Input: coins = [1, 2, 5], amount = 11
Output: 3 Explanation: 11 = 5 + 5 + 1

Example 2:
Input: coins = [2], amount = 3Output: -1


- code  BFS
```py
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        if amount == 0: return 0
        queue = [[0, 0]]
        visited = {0}
        step = 0
        for node, step in queue:
            for coin in coins:
                if node + coin == amount: return step + 1
                elif node + coin < amount and node + coin not in visited:
                    queue.append([node + coin, step + 1])
                    visited.add(node + coin)
        return -1

```
- code  dp,  F(S)=F(S−C)+1, S is the amount, C is the denomination(value of each coin)
```py
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [0] + amount*[amount+1]  # amount + 1 is the same as infinite big here
        for coin in coins:
            for i in range(coin, amount+1):
                dp[i] = min(dp[i], dp[i-coin]+1)
        return dp[amount] if dp[amount] <= amount else -1

```
 [https://leetcode.com/problems/coin-change/solution/](https://leetcode.com/problems/coin-change/solution/)
![top down](https://i.imgur.com/Sl4yAkG.png)

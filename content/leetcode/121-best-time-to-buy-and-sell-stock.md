+++
date = "2021-02-20"
title = "121. Best time to buy and sell stock"
tags = ["leetcode","dp"]
+++

You are given an array prices where prices[i] is the price of a given stock on the ith day.
You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.
Return __the maximum profit you can achieve from this transaction__. If you cannot achieve any profit, return 0.

Example 1:
Input: [7,1,5,3,6,4] Output: 5 Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.

- code
```py
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        minday = prices[0]
        maxprofit = 0
        for v in prices:
            if v < minday:
                minday = v
            else:
                maxprofit = max(maxprofit, v - minday)

        return maxprofit

```

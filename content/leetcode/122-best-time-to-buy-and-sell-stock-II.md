+++
date = "2021-01-04"
title = "122. Best time to buy and sell stock II"
tags = ["array"]
+++

Input: [7,1,5,3,6,4]  
Output: 7  
You can have as many transactions as you like.  
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
- c0
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        profit = 0
        for i in range(1, len(prices)):
            diff = prices[i] - prices[i-1]
            if diff > 0:
                profit += diff
        return profit
```
- c1
```python
                
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        length = len(prices)
        if not length:
            return 0
        profit = 0
        last = prices[0]
        for i in prices:
            if i > last:
                profit += (i-last)
            last = i
        return profit
```
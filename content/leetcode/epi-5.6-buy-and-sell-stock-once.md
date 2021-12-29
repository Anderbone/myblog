+++ 
date = "2020-12-16"
title = "Buy and sell stock once"
tags = ["array"]
+++
buy_and_sell_stock_once
notice only once  
the following sequence of stock price: (310, 315, 275, 295, 260, 270, 290..)
the maximum profit that can be made with one buy and one sell is 30. from 260 to 290  
Write a program that takes an array denoting the daily stock price, return the maximum profit that could be made by buying and then selling one share of that stock
code
- c1, same as c0
  code
```python
def buy_and_sell_stock_once(prices: List[float]) -> float:
    max_profit = 0
    buy_min = prices[0]
    for i in range(1, len(prices)):
        if prices[i] < buy_min:
            buy_min = prices[i]
        elif prices[i] > buy_min:
            if prices[i] - buy_min > max_profit:
                max_profit = prices[i] - buy_min
    return max_profit
```
- c0
  c0
```python
def buy_and_sell_stock_once(prices):
    # TODO - you fill in here.

    mini = prices[0]
    maxp = 0
    for cur in prices:
        if cur < mini:
            mini = cur
        else:
            profit = cur - mini
            maxp = max(maxp, profit)

    return maxp
```

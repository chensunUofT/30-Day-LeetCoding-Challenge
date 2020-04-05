https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/

The basic idea is to buy at low prices and sell at high points. We can use a `low` variable to keep track to the lowest price to buy, and compare the current price `p` of each day with it:
- if `p > low`, buying at `low` and selling at `p` gives us `p - low` profit, and update `low` with this `p` value. It doesn't matter if the price for next day is higher than this `p` since there's no cooldown for transactions, which means we can sell and buy at the same day.
- if `p <= low`, we just update the `low` with the `p` without buying or selling.

So a very basic solution is like:

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if len(prices) < 2:
            return 0
        profit = 0
        low = prices[0]
        for p in prices[1:]:
            if p > low:
                profit += p - low
                low = p
            else:
                low = p
        return profit
    
```

Note that we are updating the  `low` variable anyway in each iteration, we can actually visit the value with index instead of using the variable to keep track of it.

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if len(prices) < 2:
            return 0
        profit = 0
        for i in range(1, len(prices)):
            if prices[i] > prices[i-1]:
                profit += prices[i] - prices[i-1]
        return profit
    
```

To pack it in one line:

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        return sum([max(prices[i]-prices[i-1], 0) for i in range(1, len(prices))])
```


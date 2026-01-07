# 40. Best Time To Buy And Sell Stock With Transaction Fee

## Solution

## 1) Space Optimization

```cpp
#include<bits/stdc++.h>

int maximumProfit(vector<int> &prices, int n, int fee)
{
	vector<long> ahead(2, 0), curr(2, 0);

    for (int ind=n-1; ind>=0; ind--) {
        long buy = -prices[ind] + ahead[0];
        long notBuy = ahead[1];

        curr[1] = max(buy, notBuy);

        long sell = prices[ind] - fee + ahead[1];
        long notSell = ahead[0];

        curr[0] = max(sell, notSell);

        ahead = curr;
    }

    return ahead[1];
}
```

## Analysis

- **Time Complexity**: `O(n * 2)`
- **Space Complexity**: `O(1)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/best-time-to-buy-and-sell-stock-with-transaction-fee_3118974

## Tags

#dp #recursion #stocks 
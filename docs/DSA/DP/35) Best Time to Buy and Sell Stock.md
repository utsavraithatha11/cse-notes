## Description

- Can be traded only once.

## Solutions

```cpp
#include <bits/stdc++.h> 
int maximumProfit(vector<int> &prices){
    int mini = prices[0], profit = 0;

    for (int i=1; i<prices.size(); i++) {
        profit = max(profit, prices[i] - mini);
        mini = min(mini, prices[i]);
    }

    return profit;
}
```

## Analysis

- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(1)`

---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/stocks-are-profitable_893405

## Tags

#dp #stocks 
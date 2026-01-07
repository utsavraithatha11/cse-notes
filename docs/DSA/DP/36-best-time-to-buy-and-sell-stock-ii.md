# 36. Best Time To Buy And Sell Stock - II

## Description

- Can be traded multiple times.

## Solutions
## 1) Memorization

```cpp
#include<bits/stdc++.h>

int N;

long solve(int ind, int buyAllowed, long *values, vector<vector<long>> &dp) {
    if (ind == N) return 0;

    if (dp[ind][buyAllowed] != -1) return dp[ind][buyAllowed];

    if (buyAllowed == 0) {
        long sell = values[ind] + solve(ind+1, 1, values, dp);
        long notSell = solve(ind+1, 0, values, dp);

        return dp[ind][buyAllowed] = max(sell, notSell);
    }
    else {
        long buy = -values[ind] + solve(ind+1, 0, values, dp);
        long notBuy = solve(ind+1, 1, values, dp);
        return dp[ind][buyAllowed] = max(buy, notBuy);
    }
}

long getMaximumProfit(long *values, int n)
{
    N = n;
    vector<vector<long>> dp(n, vector<long> (2, -1));

    return solve(0, 1, values, dp);
}
```

## Analysis

- **Time Complexity**: `O(n * 2)`
- **Space Complexity**: `O(n * 2) + O(n)`

---

## 2) Tabulation

```cpp
#include<bits/stdc++.h>

long getMaximumProfit(long *values, int n)
{
    vector<vector<long>> dp(n+1, vector<long> (2, 0));

    for (int ind=n-1; ind>=0; ind--) {
        long buy = -values[ind] + dp[ind+1][0];
        long notBuy = dp[ind+1][1];

        dp[ind][1] = max(buy, notBuy);

        long sell = values[ind] + dp[ind+1][1];
        long notSell = dp[ind+1][0];

        dp[ind][0] = max(sell, notSell);
    }

    return dp[0][1];
}
```

## Analysis

- **Time Complexity**: `O(n * 2)`
- **Space Complexity**: `O(n * 2)`

---

## 3) Space Optimization

```cpp
#include<bits/stdc++.h>

long getMaximumProfit(long *values, int n)
{
    vector<long> ahead(2, 0), curr(2, 0);

    for (int ind=n-1; ind>=0; ind--) {
        long buy = -values[ind] + ahead[0];
        long notBuy = ahead[1];

        curr[1] = max(buy, notBuy);

        long sell = values[ind] + ahead[1];
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

- **Problem Link**: https://www.naukri.com/code360/problems/best-time-to-buy-and-sell-stock-ii_630282

## Tags

#dp #recursion #stocks 
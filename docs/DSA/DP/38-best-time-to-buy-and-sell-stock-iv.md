## Description

- Allowed at most K transactions.
- Same as 37.

## Solutions

## 1) Space Optimization

```cpp
#include <bits/stdc++.h> 

int maximumProfit(vector<int> &prices, int n, int k)
{
    vector<vector<int>> ahead(2, vector<int> (k+1, 0));
    vector<vector<int>> curr(2, vector<int> (k+1, 0));

    for (int ind=n-1; ind>=0; ind--) {
        for (int buyAllowed=0; buyAllowed<=1; buyAllowed++) {
            for (int rem=1; rem<=k; rem++) {
                if (buyAllowed) {
                    int buy = -prices[ind] + ahead[0][rem];
                    int notBuy = ahead[1][rem];

                    curr[buyAllowed][rem] = max(buy, notBuy);
                } 
                else {
                    int sell = prices[ind] + ahead[1][rem-1];
                    int notSell = ahead[0][rem];

                    curr[buyAllowed][rem] = max(sell, notSell);
                }
            }
        }

        ahead = curr;
    }

    return ahead[1][k];
}
```

## Analysis

- **Time Complexity**: `O(n * 2 * k)`
- **Space Complexity**: `O(k)`


# Another Approach (Transaction Method)

- Even transaction no. means BUY, odd means SELL

### 1) Memoization


```cpp
#include <bits/stdc++.h> 

int solve(int ind, int tranNo, vector<int> &prices, int &n, int &k, vector<vector<int>> &dp) {
    if (ind == n || tranNo == 2*k) return 0;

    if (dp[ind][tranNo] != -1) return dp[ind][tranNo];

    // buy
    if (tranNo % 2 == 0) {
        return dp[ind][tranNo] = max(-prices[ind] + solve(ind+1, tranNo+1, prices, n, k, dp),
                                solve(ind+1, tranNo, prices, n, k, dp));
    }
    else {
        return dp[ind][tranNo] = max(prices[ind] + solve(ind+1, tranNo+1, prices, n, k, dp),
                                solve(ind+1, tranNo, prices, n, k, dp));
    }
}

int maximumProfit(vector<int> &prices, int n, int k)
{
    vector<vector<int>> dp(n, vector<int> (2*k, -1));
    return solve(0, 0, prices, n, k, dp);
}

```

## Analysis

- **Time Complexity**: `O(n * 2 * k)`
- **Space Complexity**: `O(n * 2 * k) + O(n)`

---

### 2) Tabulation


```cpp
#include <bits/stdc++.h> 

int maximumProfit(vector<int> &prices, int n, int k)
{
    vector<vector<int>> dp(n+1, vector<int> (2*k+1, 0));

    for (int ind=n-1; ind>=0; ind--) {
        for (int tranNo=0; tranNo<=2*k-1; tranNo++) {
            if (tranNo % 2 == 0) {
                dp[ind][tranNo] = max(-prices[ind] + dp[ind+1][tranNo+1], dp[ind+1][tranNo]);
            }
            else {
                dp[ind][tranNo] = max(prices[ind] + dp[ind+1][tranNo+1], dp[ind+1][tranNo]);
            }
        }
    }
    return dp[0][0];
}
```

## Analysis

- **Time Complexity**: `O(n * 2 * k)`
- **Space Complexity**: `O(n * 2 * k)`


--- 

### 3) Space Optimization


```cpp
#include <bits/stdc++.h> 

int maximumProfit(vector<int> &prices, int n, int k)
{
    vector<int> ahead(2*k+1, 0), curr(2*k+1, 0);

    for (int ind=n-1; ind>=0; ind--) {
        for (int tranNo=0; tranNo<=2*k-1; tranNo++) {
            if (tranNo % 2 == 0) {
                curr[tranNo] = max(-prices[ind] + ahead[tranNo+1], ahead[tranNo]);
            }
            else {
                curr[tranNo] = max(prices[ind] + ahead[tranNo+1], ahead[tranNo]);
            }
        }

        ahead = curr;
    }
    return ahead[0];
}
```

## Analysis

- **Time Complexity**: `O(n * 2 * k)`
- **Space Complexity**: `O(k)`

---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/best-time-to-buy-and-sell-stock_1080698

## Tags

#dp #recursion #stocks 
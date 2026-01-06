## Description

- Can be traded only 2 times maximum.

## Solutions
## 1) Memorization

```cpp
#include<bits/stdc++.h>

int solve(int ind, int buyAllowed, int rem, vector<int> &prices, int &n, vector<vector<vector<int>>> &dp) {
    if (ind == n || rem == 0) return 0;

    if (dp[ind][buyAllowed][rem] != -1) return dp[ind][buyAllowed][rem];

    if (buyAllowed) {
        int buy = -prices[ind] + solve(ind+1, 0, rem, prices, n, dp);
        int notBuy = solve(ind+1, 1, rem, prices, n, dp);

        return dp[ind][buyAllowed][rem] = max(buy, notBuy);
    } 
    else {
        int sell = prices[ind] + solve(ind+1, 1, rem-1, prices, n, dp);
        int notSell = solve(ind+1, 0, rem, prices, n, dp);

        return dp[ind][buyAllowed][rem] = max(sell, notSell);
    }
}

int maxProfit(vector<int>& prices)
{
    int n = prices.size();
    vector<vector<vector<int>>> dp(n+1, vector<vector<int>> (2, vector<int> (3, -1)));

    return solve(0, 1, 2, prices, n, dp);
}
```

## Analysis

- **Time Complexity**: `O(n * 2 * 3)`
- **Space Complexity**: `O(n * 2 * 3) + O(n)`


---

## 2) Tabulation

```cpp
#include<bits/stdc++.h>

int maxProfit(vector<int>& prices)
{
    int n = prices.size();
    vector<vector<vector<int>>> dp(n+1, vector<vector<int>> (2, vector<int> (3, 0)));

    for (int ind=n-1; ind>=0; ind--) {
        for (int buyAllowed=0; buyAllowed<=1; buyAllowed++) {
            for (int rem=1; rem<=2; rem++) {
                if (buyAllowed) {
                    int buy = -prices[ind] + dp[ind+1][0][rem];
                    int notBuy = dp[ind+1][1][rem];

                    dp[ind][buyAllowed][rem] = max(buy, notBuy);
                } 
                else {
                    int sell = prices[ind] + dp[ind+1][1][rem-1];
                    int notSell = dp[ind+1][0][rem];

                    dp[ind][buyAllowed][rem] = max(sell, notSell);
                }
            }
        }
    }

    return dp[0][1][2];
}
```

## Analysis

- **Time Complexity**: `O(n * 2 * 3)`
- **Space Complexity**: `O(n * 2 * 3)`


---

## 3) Space Optimization

```cpp
#include<bits/stdc++.h>

int maxProfit(vector<int>& prices)
{
    int n = prices.size();
    vector<vector<int>> ahead(2, vector<int> (3, 0));
    vector<vector<int>> curr(2, vector<int> (3, 0));

    for (int ind=n-1; ind>=0; ind--) {
        for (int buyAllowed=0; buyAllowed<=1; buyAllowed++) {
            for (int rem=1; rem<=2; rem++) {
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

    return ahead[1][2];
}
```

## Analysis

- **Time Complexity**: `O(n * 2 * 3)`
- **Space Complexity**: `O(1)`

---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/best-time-to-buy-and-sell-stock-iii_1071012

## Tags

#dp #recursion #stocks 
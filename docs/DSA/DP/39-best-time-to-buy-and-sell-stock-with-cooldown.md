# 39. Best Time To Buy And Sell Stock With Cooldown

## Description

- After sell call omit 1 index

## Solutions
## 1) Memorization

```cpp
class Solution {
public:

    int solve(int ind, int buyAllowed, vector<int> &prices, vector<vector<int>> &dp) {
        if (ind >= prices.size()) return 0;

        if (dp[ind][buyAllowed] != -1) return dp[ind][buyAllowed];

        if (buyAllowed) {
            return dp[ind][buyAllowed] = max(
                -prices[ind] + solve(ind+1, 0, prices, dp),
                solve(ind+1, 1, prices, dp)
            );
        }
        else {
            return dp[ind][buyAllowed] = max(
                prices[ind] + solve(ind+2, 1, prices, dp),
                solve(ind+1, 0, prices, dp)
            );
        }
    }

    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<int>> dp(n, vector<int> (2, -1));
        return solve(0, 1, prices, dp);
    }
};
```

## Analysis

- **Time Complexity**: `O(n * 2)`
- **Space Complexity**: `O(n * 2) + O(n)`



---

## 2) Tabulation

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<int>> dp(n+2, vector<int> (2, 0));
        
        for (int ind=n-1; ind>=0; ind--) {
            dp[ind][1] = max(-prices[ind] + dp[ind+1][0], dp[ind+1][1]);
            dp[ind][0] = max(prices[ind] + dp[ind+2][1], dp[ind+1][0]);
        }

        return dp[0][1];
    }
};
```

## Analysis

- **Time Complexity**: `O(n * 2)`
- **Space Complexity**: `O(n * 2)`


---

## 3) Space Optimization

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<int> front2(2, 0);
        vector<int> front1(2, 0);
        vector<int> curr(2, 0);
        
        for (int ind=n-1; ind>=0; ind--) {
            curr[1] = max(-prices[ind] + front1[0], front1[1]);
            curr[0] = max(prices[ind] + front2[1], front1[0]);

            front2 = front1;
            front1 = curr;
        }

        return curr[1];
    }
};
```

## Analysis

- **Time Complexity**: `O(n * 2)`
- **Space Complexity**: `O(1)`


---

## Resources

- **Problem Link**: https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/

## Tags

#dp #recursion #stocks 
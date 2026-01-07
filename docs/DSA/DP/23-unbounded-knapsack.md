# 23. Unbounded Knapsack

## Description

- Allowed to take one of the sack multiple times

## Solutions
## 1) Memorization

```cpp
#include<bits/stdc++.h>

int solve(int i, int rem, vector<int> &profit, vector<int> &weight, vector<vector<int>> &dp) {
    if (i == 0) {
        return profit[0] * (rem / weight[i]);
    }

    if (dp[i][rem] != -1) return dp[i][rem];

    int notTake = solve(i-1, rem, profit, weight, dp);
    int take = 0;
    if (weight[i] <= rem) {
        take = profit[i] + solve(i, rem - weight[i], profit, weight, dp);
    }

    return dp[i][rem] = max(take, notTake);
}

int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight){
    vector<vector<int>> dp(n, vector<int> (w + 1, -1));

    return solve(n-1, w, profit, weight, dp);
}
```

## Analysis

-  **Time Complexity**: `O(n * target)`
- **Space Complexity**: `O(n * target) + O(n)`

---

## 2) Tabulation

```cpp
#include<bits/stdc++.h>

int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight){
    vector<vector<int>> dp(n, vector<int> (w + 1, 0));

    for (int i=0; i<=w; i++) {
        dp[0][w] = (w / weight[0]) * profit[0];
    }

    for (int i=1; i<n; i++) {
        for (int rem=0; rem<=w; rem++) {
            int notTake = dp[i-1][rem];
            int take = 0;
            if (weight[i] <= rem) take = profit[i] + dp[i][rem - weight[i]];

            dp[i][rem] = max(take, notTake);
        }
    }

    return dp[n-1][w];
}
```

## Analysis

-  **Time Complexity**: `O(n * target)`
- **Space Complexity**: `O(n * target)`


---

## 3) Space Optimization

```cpp
#include<bits/stdc++.h>

int unboundedKnapsack(int n, int w, vector<int> &profit, vector<int> &weight){
    vector<int> prev(w+1, 0), curr(w+1, 0);

    for (int i=0; i<=w; i++) {
        prev[w] = (w / weight[0]) * profit[0];
    }

    for (int i=1; i<n; i++) {
        for (int rem=0; rem<=w; rem++) {
            int notTake = prev[rem];
            int take = 0;
            if (weight[i] <= rem) take = profit[i] + curr[rem - weight[i]];

            curr[rem] = max(take, notTake);
        }

        prev = curr;
    }

    return prev[w];
}
```

## Analysis

-  **Time Complexity**: `O(n * target)`
- **Space Complexity**: `O(target)`

---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/unbounded-knapsack_1215029

## Tags


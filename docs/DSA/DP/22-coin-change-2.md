# 22. Coin Change 2

## Description

- Count total ways to make coins sum equal to Target
- Duplicate coins allowed

## Solutions
## 1) Memorization

```cpp
#include <bits/stdc++.h>

long solve(int ind, int sum, int *denominations, int n, vector<vector<long>> &dp) {
    if (ind == 0) {
        return (sum % denominations[0] == 0);
    }

    if (dp[ind][sum] != -1) return dp[ind][sum];

    long notTake = solve(ind-1, sum, denominations, n, dp);
    long take = 0;
    if (denominations[ind] <= sum) take = solve(ind, sum - denominations[ind], denominations, n, dp);

    return dp[ind][sum] = take + notTake;
}

long countWaysToMakeChange(int *denominations, int n, int value) {
    vector<vector<long>> dp(n, vector<long> (value + 1, -1));

    return solve(n-1, value, denominations, n, dp);
}
```

## Analysis

-  **Time Complexity**: `O(n * target)`
- **Space Complexity**: `O(n * target) + O(n)`


---

## 2) Tabulation

```cpp
#include <bits/stdc++.h>

long countWaysToMakeChange(int *denominations, int n, int value) {
    vector<vector<long>> dp(n, vector<long> (value + 1, 0));

    for (int i=0; i<=value; i++) {
        dp[0][i] = (value % denominations[0] == 0);
    }

    for (int i=1; i<n; i++) {
        for (int tar=0; tar<=value; tar++) {
            long notTake = dp[i-1][tar];
            long take = 0;
            if (denominations[i] <= tar) take = dp[i][tar - denominations[i]];

            dp[i][tar] = take + notTake;
        }
    }
    
    return dp[n-1][value];
}
```

## Analysis

- **Time Complexity**: `O(n * target)`
- **Space Complexity**: `O(n * target)`


---

## 3) Space Optimization

```cpp
#include <bits/stdc++.h>

long countWaysToMakeChange(int *denominations, int n, int value) {
    vector<long> dp(value + 1, 0);

    for (int i=0; i<=value; i++) {
        dp[i] = (value % denominations[0] == 0);
    }

    for (int i=1; i<n; i++) {
        vector<long> curr(value + 1, 0);
        for (int tar=0; tar<=value; tar++) {
            long notTake = dp[tar];
            long take = 0;
            if (denominations[i] <= tar) take = curr[tar - denominations[i]];

            curr[tar] = take + notTake;
        }

        dp = curr;
    }
    
    return dp[value];
}
```

## Analysis

-  **Time Complexity**: `O(n * target)`
- **Space Complexity**: `O(target)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/ways-to-make-coin-change_630471

## Tags

#dp #recursion #take-not-take #count
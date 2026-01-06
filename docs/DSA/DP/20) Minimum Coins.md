## Description

- Take minimum coins from the available denominations that sum to target.

## Solutions
## 1) Memorization

```cpp
#include <bits/stdc++.h>

int solve(int ind, int tar, vector<int> &num, vector<vector<int>> &dp) {
    if (ind == 0) {
        if (tar % num[0] == 0) return tar / num[0];
        return 1e9;
    }

    if (dp[ind][tar] != -1) return dp[ind][tar];

    int notTake = solve(ind-1, tar, num, dp);
    int take = 1e9;
    if (num[ind] <= tar) take = 1 + solve(ind, tar-num[ind], num, dp);

    return dp[ind][tar] = min(take, notTake);
}

int minimumElements(vector<int> &num, int x) {
    int n = num.size();
    vector<vector<int>> dp(n, vector<int> (x+1, -1));

    int ans = solve(n-1, x, num, dp);
    return ans >= 1e9 ? -1: ans;
}
```

## Analysis

- **Time Complexity**: `O(n * target)`
- **Space Complexity**: `O(n * target) + O(n)`

---

## 2) Tabulation

```cpp
#include <bits/stdc++.h>

int minimumElements(vector<int> &num, int x) {
    int n = num.size();
    vector<vector<int>> dp(n, vector<int> (x+1, 0));

    // base-case
    for (int tar=0; tar<=x; tar++) {
        if (tar % num[0] == 0) dp[0][tar] = tar / num[0];
        else dp[0][tar] = 1e9;
    }

    for (int i=1; i<n; i++) {
        for (int tar=0; tar<=x; tar++) {
            int notTake = dp[i-1][tar];
            int take = 1e9;
            if (num[i] <= tar) take = 1 + dp[i][tar-num[i]];

            dp[i][tar] = min(take, notTake);
        }
    }

    int ans = dp[n-1][x];
    return ans >= 1e9 ? -1: ans;
}
```

## Analysis

- **Time Complexity**: `O(n * target)`
- **Space Complexity**: `O(n * target)`


---

## 3) Space Optimization

```cpp
#include <bits/stdc++.h>

int minimumElements(vector<int> &num, int x) {
    int n = num.size();
    vector<int> prev(x+1, 0), curr(x+1, 0);

    // base-case
    for (int tar=0; tar<=x; tar++) {
        if (tar % num[0] == 0) prev[tar] = tar / num[0];
        else prev[tar] = 1e9;
    }

    for (int i=1; i<n; i++) {
        for (int tar=0; tar<=x; tar++) {
            int notTake = prev[tar];
            int take = 1e9;
            if (num[i] <= tar) take = 1 + curr[tar-num[i]];

            curr[tar] = min(take, notTake);
        }
        prev = curr;
    }

    int ans = prev[x];
    return ans >= 1e9 ? -1: ans;
}
```

## Analysis

- **Time Complexity**: `O(n * target)`
- **Space Complexity**: `O(target)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/minimum-elements_3843091 

## Tags

#dp #recursion #take-not-take #minimization
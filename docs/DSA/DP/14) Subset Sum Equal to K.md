## Description

- Check if any subset sums to K or not.

## Solutions
## 1) Memorization

```cpp
#include <bits/stdc++.h> 

bool solve(int ind, int target, vector<int> &arr, vector<vector<int>> &dp) {
    if (target == 0) return true;

    if (ind == 0) return arr[0] == target;

    if (dp[ind][target] != -1) return dp[ind][target];

    bool notTake = solve(ind - 1, target, arr, dp);
    bool take = false;

    if (target >= arr[ind])
        take = solve(ind - 1, target - arr[ind], arr, dp);

    return dp[ind][target] = take | notTake;
}

bool subsetSumToK(int n, int k, vector<int> &arr) {
    vector<vector<int>> dp(n, vector<int> (k+1, -1));

    return solve(n-1, k, arr, dp);   
}
```

## Analysis

- **Time Complexity**: `O(n * target)`
- **Space Complexity**: `O(n * target) + O(n)`

---

## 2) Tabulation

```cpp
#include <bits/stdc++.h> 

bool subsetSumToK(int n, int k, vector<int> &arr) {
    vector<vector<bool>> dp(n, vector<bool> (k+1, 0));

    // base cases
    for (int i=0; i<n; i++) dp[i][0] = true;
    if (arr[0] <= k) dp[0][arr[0]] = true;

    for (int i=1; i<n; i++) {
        for (int target = 1; target <= k; target++) {
            bool notTake = dp[i-1][target];
            bool take = false;
            if (target >= arr[i]) take = dp[i-1][target-arr[i]];

            dp[i][target] = take | notTake;
        }
    }

    return dp[n-1][k];
}
```

## Analysis

- **Time Complexity**: `O(n * target)`
- **Space Complexity**: `O(n * target)`

---

## 3) Space Optimization

```cpp
#include <bits/stdc++.h> 

bool subsetSumToK(int n, int k, vector<int> &arr) {
    vector<bool> prev(k+1, 0), curr(k+1, 0);

    // base cases
    prev[0] = true;
    if (arr[0] <= k) prev[arr[0]] = true;
    curr[0] = true;

    for (int i=1; i<n; i++) {
        for (int target = 1; target <= k; target++) {
            bool notTake = prev[target];
            bool take = false;
            if (target >= arr[i]) take = prev[target-arr[i]];

            curr[target] = take | notTake;
        }

        prev = curr;
    }

    return prev[k];
}
```

## Analysis

- **Time Complexity**: `O(n * target)`
- **Space Complexity**: `O(target)`

---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/subset-sum-equal-to-k_1550954

## Tags

#dp #recursion #sum #subsequence #subset #subset-sum 
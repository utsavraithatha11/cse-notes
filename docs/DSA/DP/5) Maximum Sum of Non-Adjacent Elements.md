## Solutions
## 1) Memorization

```cpp
#include <bits/stdc++.h>

int solve(int ind, vector<int> &nums, vector<int> &dp) {
    if (ind == 0) return nums[ind];

    if (ind < 0) return 0;

    if (dp[ind] != -1) return dp[ind];

    int pick = nums[ind] + solve(ind - 2, nums, dp);
    int notPick = solve(ind - 1, nums, dp);

    return dp[ind] = max(pick, notPick);
}

int maximumNonAdjacentSum(vector<int> &nums){
    int n = nums.size();
    vector<int> dp(n, -1);

    return solve(n-1, nums, dp);
}
```

## Analysis

- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(n) + O(n)`


---

## 2) Tabulation

```cpp
#include <bits/stdc++.h>

int maximumNonAdjacentSum(vector<int> &nums){
    int n = nums.size();
    vector<int> dp(n);
    dp[0] = nums[0];

    for (int i=1; i<n; i++) {
        int take = nums[i];
        if (i > 1) take += dp[i-2];

        int notTake = dp[i-1];

        dp[i] = max(take, notTake);
    }

    return dp[n-1];
}
```

## Analysis

- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(n)`


---

## 3) Space Optimization

```cpp
#include <bits/stdc++.h>

int maximumNonAdjacentSum(vector<int> &nums){
    int n = nums.size();
    int prev2 = 0, prev = nums[0];
    int curr;

    for (int i=1; i<n; i++) {
        int take = nums[i];
        if (i > 1) take += prev2;

        int notTake = prev;

        curr = max(take, notTake);
        prev2 = prev;
        prev = curr;
    }

    return prev;
}
```

## Analysis

- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(1)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/maximum-sum-of-non-adjacent-elements_843261

## Tags

#recursion #dp #sum #maximization #take-not-take 

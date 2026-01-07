# 3. Frog Jump

## Description

- Frog can jump from one building to other with the energy of abs(heights[i] - heights[j]).
- Frog can jump 1 or 2 buildings at a time.
- Find minimum energy to go from 1st to Nth building.

## Solutions
## 1) Memorization

```cpp
#include <bits/stdc++.h>

int solve(int ind, vector<int> &heights, vector<int> &dp) {
    if (ind == 0) return 0;

    if (dp[ind] != -1) return dp[ind];

    int left = solve(ind - 1, heights, dp) + abs(heights[ind] - heights[ind - 1]);
    
    int right = INT_MAX;
    if (ind > 1) right = solve(ind - 2, heights, dp) + abs(heights[ind] - heights[ind - 2]);

    return dp[ind] = min(left, right);
}

int frogJump(int n, vector<int> &heights)
{
    vector<int> dp(n, -1);
    return solve(n - 1, heights, dp);
}
```

## Analysis

- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(n) + O(n)`


---

## 2) Tabulation

```cpp
#include <bits/stdc++.h>

int frogJump(int n, vector<int> &heights)
{
    vector<int> dp(n);
    dp[0] = 0;

    for (int i=1; i<n; i++) {
        int fs = dp[i-1] + abs(heights[i] - heights[i-1]);
        int ss = INT_MAX;
        if (i > 1) ss = dp[i-2] + abs(heights[i] - heights[i - 2]);

        dp[i] = min(fs, ss);
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

int frogJump(int n, vector<int> &heights)
{
    int prev2 = 0, prev = 0;
    int curr;

    for (int i=1; i<n; i++) {
        int fs = prev + abs(heights[i] - heights[i-1]);
        int ss = INT_MAX;
        if (i > 1) ss = prev2 + abs(heights[i] - heights[i - 2]);

        curr = min(fs, ss);
        prev2 = prev;
        prev = curr;
    }

    return curr;
}
```

## Analysis

- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(1)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/frog-jump_3621012

## Tags

#dp #recursion
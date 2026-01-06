## Description

- Here, k jumps are allowed.

## Solution

```cpp
#include <bits/stdc++.h>

int frogJump(int n, int k, vector<int> &heights)
{
    vector<int> dp(n, INT_MAX);
    dp[0] = 0;

    for (int i=1; i<n; i++) {
        for (int j=1; j<=k; j++) {
            if (i-j >= 0) {
                dp[i] = min(dp[i], dp[i-j] + abs(heights[i] - heights[i-j]));
            } else {
                break;
            }
        }
    }

    return dp[n-1];
}
```

## Analysis

- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(n)`

## Tags

#recursion #dp 
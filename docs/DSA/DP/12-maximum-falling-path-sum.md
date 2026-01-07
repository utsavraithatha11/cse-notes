# 12. Maximum Falling Path Sum

## Description

- Start from any cell in first row and reach any cell in last row to maximize sum.

## Solutions
## 1) Memorization

```cpp
#include <bits/stdc++.h> 

int n, m;

int solve(int i, int j, vector<vector<int>> &matrix, vector<vector<int>> &dp) {
    if (j >= m || j < 0) return -1e6;

    if (i == 0) return matrix[i][j];

    if (dp[i][j] != -1) return dp[i][j];

    int u = matrix[i][j] + solve(i-1, j, matrix, dp);
    int ld = matrix[i][j] + solve(i-1, j-1, matrix, dp);
    int rd = matrix[i][j] + solve(i-1, j+1, matrix, dp);

    return dp[i][j] = max({u, ld, rd});
}

int getMaxPathSum(vector<vector<int>> &matrix)
{
    n = matrix.size();
    m = matrix[0].size();

    vector<vector<int>> dp(n, vector<int> (m, -1));

    int ans = -1e6;

    for (int j=0; j<m; j++) {
        ans = max(ans, solve(n-1, j, matrix, dp));
    }

    return ans;
}
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(n * m) + O(n)`


---

## 2) Tabulation

```cpp
#include <bits/stdc++.h> 

int getMaxPathSum(vector<vector<int>> &matrix)
{
    int n = matrix.size();
    int m = matrix[0].size();

    vector<vector<int>> dp(n, vector<int> (m, 0));

    // base case
    for (int j=0; j<m; j++) {
        dp[0][j] = matrix[0][j];
    }

    for (int i=1; i<n; i++) {
        for (int j=0; j<m; j++) {
            int u = -1e6, ld = -1e6, rd = -1e6;

            u = matrix[i][j] + dp[i-1][j];
            if (j-1 >= 0) ld = matrix[i][j] + dp[i-1][j-1];
            if (j+1 < m) rd = matrix[i][j] + dp[i-1][j+1];

            dp[i][j] = max({u, ld, rd});
        }
    }

    int ans = -1e6;

    for (int j=0; j<m; j++) {
        ans = max(ans, dp[n-1][j]);
    }

    return ans;
}
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(n * m)`

## Notes



---

## 3) Space Optimization

```cpp
#include <bits/stdc++.h> 

int getMaxPathSum(vector<vector<int>> &matrix)
{
    int n = matrix.size();
    int m = matrix[0].size();

    vector<int> prev(m, 0), curr(m, 0);

    // base case
    for (int j=0; j<m; j++) {
        prev[j] = matrix[0][j];
    }

    for (int i=1; i<n; i++) {
        for (int j=0; j<m; j++) {
            int u = -1e6, ld = -1e6, rd = -1e6;

            u = matrix[i][j] + prev[j];
            if (j-1 >= 0) ld = matrix[i][j] + prev[j-1];
            if (j+1 < m) rd = matrix[i][j] + prev[j+1];

            curr[j] = max({u, ld, rd});
        }

        prev = curr;
    }

    int ans = -1e6;

    for (int j=0; j<m; j++) {
        ans = max(ans, prev[j]);
    }

    return ans;
}
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(m)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/maximum-path-sum-in-the-matrix_797998

## Tags

#dp #recursion #sum #maximization #grid 
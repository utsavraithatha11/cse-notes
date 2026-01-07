
## Solutions
## 1) Memorization

```cpp
#include <bits/stdc++.h>

int solve(int i, int j, vector<vector<int>> &grid, vector<vector<int>> &dp) {
    if (i == 0 && j == 0) return grid[i][j];

    if (i < 0 || j < 0) return 1e9;

    if (dp[i][j] != -1) return dp[i][j];

    int up = grid[i][j] + solve(i-1, j, grid, dp);
    int left = grid[i][j] + solve(i, j-1, grid, dp);
    
    return dp[i][j] = min(up, left);
}

int minSumPath(vector<vector<int>> &grid) {
    int n = grid.size();
    int m = grid[0].size();
    vector<vector<int>> dp(n, vector<int> (m, -1));

    return solve(n-1, m-1, grid, dp);
}
```

## Analysis

- **Time Complexity**: `O(m * n)`
- **Space Complexity**: `O(path length) + O(m * n) = O(m - 1 + n - 1) + O(m * n)``


---

## 2) Tabulation

```cpp
#include <bits/stdc++.h>

int minSumPath(vector<vector<int>> &grid) {
    int n = grid.size();
    int m = grid[0].size();

    vector<vector<int>> dp(n, vector<int> (m, 0));
    dp[0][0] = grid[0][0];

    for (int i=0; i<n; i++) {
        for (int j=0; j<m; j++) {
            if (i == 0 && j == 0) continue;
            else {
                int up = 1e9, left = 1e9;
                if (i > 0) up = grid[i][j] + dp[i-1][j];
                if (j > 0) left = grid[i][j] + dp[i][j-1];

                dp[i][j] = min(up, left);
            }
        }
    }

    return dp[n-1][m-1];
}
```

## Analysis

- **Time Complexity**: `O(m * n)`
- **Space Complexity**: `O(m * n) `


---

## 3) Space Optimization

```cpp
#include <bits/stdc++.h>

int minSumPath(vector<vector<int>> &grid) {
    int n = grid.size();
    int m = grid[0].size();

    vector<int> prev_row(m, 0);

    for (int i=0; i<n; i++) {
        vector<int> row(m, 0);
        for (int j=0; j<m; j++) {
            if (i == 0 && j == 0) row[0] = grid[i][j];
            else {
                int up = 1e9, left = 1e9;
                if (i > 0) up = grid[i][j] + prev_row[j];
                if (j > 0) left = grid[i][j] + row[j-1];

                row[j] = min(up, left);
            }
        }

        prev_row = row;
    }

    return prev_row[m-1];
}
```

## Analysis

- **Time Complexity**: `O(m * n)`
- **Space Complexity**: `O(m)`

---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/minimum-path-sum_985349

## Tags

#dp #recursion #sum #grid 
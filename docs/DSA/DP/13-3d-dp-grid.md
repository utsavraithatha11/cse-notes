# 13. 3D DP - Grid

## Description

- Alice starts from (0,0) and bob starts from (0, c-1)
- Both can go down or diagonally down.
- Maximize sum (if both go in same cell, count only once)

## Solutions
## 1) Memorization

```cpp
#include <bits/stdc++.h> 

int solve(int i, int j1, int j2, int r, int c, vector<vector<int>> &grid, vector<vector<vector<int>>> &dp) {
    
    // base cases
    if (j1 < 0 || j1 >= c || j2 < 0 || j2 >= c) return -1e9;

    if (i == r-1) {
        if (j1 == j2) return grid[i][j1];
        else return grid[i][j1] + grid[i][j2];
    }

    if (dp[i][j1][j2] != -1) return dp[i][j1][j2];

    // explore all paths of alice and bob simultaneously
    
    int maxi = 0;

    for (int d1 = -1; d1 <= 1; d1++) {
        for (int d2 = -1; d2 <= 1; d2++) {
            int value = 0;

            if (j1 == j2) value += grid[i][j1];
            else value += grid[i][j1] + grid[i][j2];

            value += solve(i+1, j1+d1, j2+d2, r, c, grid, dp);

            maxi = max(maxi, value);
        }
    }

    return dp[i][j1][j2] = maxi;
}

int maximumChocolates(int r, int c, vector<vector<int>> &grid) {
    vector<vector<vector<int>>> dp(r, vector<vector<int>> (c, vector<int> (c, -1)));
    return solve(0, 0, c-1, r, c, grid, dp);
}
```

## Analysis

- **Time Complexity**: `O(r * c * c) * 9`
- **Space Complexity**: `O(r * c * c) + O(r)`


---

## 2) Tabulation

```cpp
#include <bits/stdc++.h> 

int maximumChocolates(int r, int c, vector<vector<int>> &grid) {
    vector<vector<vector<int>>> dp(r, vector<vector<int>> (c, vector<int> (c, 0)));

    // base case
    for (int j1 = 0; j1 < c; j1++) {
        for (int j2 = 0; j2 < c; j2++) {
            if (j1 == j2) dp[r-1][j1][j2] = grid[r-1][j1];
            else dp[r-1][j1][j2] = grid[r-1][j1] + grid[r-1][j2];
        }
    }

    for (int i=r-2; i>=0; i--) {
        for (int j1=0; j1<c; j1++) {
            for (int j2=0; j2<c; j2++) {
                int maxi = 0;

                for (int d1 = -1; d1 <= 1; d1++) {
                    for (int d2 = -1; d2 <= 1; d2++) {
                        int value = 0;

                        if (j1 == j2) value += grid[i][j1];
                        else value += grid[i][j1] + grid[i][j2];

                        if (j1+d1 >= 0 && j1+d1 < c && j2+d2 >= 0 && j2+d2 < c)
                            value += dp[i+1][j1+d1][j2+d2];
                        else 
                            value += -1e9;

                        maxi = max(maxi, value);
                    }
                } 

                dp[i][j1][j2] = maxi;
            }
        }
    }

    return dp[0][0][c-1];
}
```

## Analysis

- **Time Complexity**: `O(r * c * c) * 9`
- **Space Complexity**: `O(r * c * c)`


---

## 3) Space Optimization

```cpp
#include <bits/stdc++.h> 

int maximumChocolates(int r, int c, vector<vector<int>> &grid) {
    vector<vector<int>> prev(c, vector<int> (c, 0));
    vector<vector<int>> curr(c, vector<int> (c, 0));
    
    // base case
    for (int j1 = 0; j1 < c; j1++) {
        for (int j2 = 0; j2 < c; j2++) {
            if (j1 == j2) prev[j1][j2] = grid[r-1][j1];
            else prev[j1][j2] = grid[r-1][j1] + grid[r-1][j2];
        }
    }

    for (int i=r-2; i>=0; i--) {
        for (int j1=0; j1<c; j1++) {
            for (int j2=0; j2<c; j2++) {
                int maxi = 0;

                for (int d1 = -1; d1 <= 1; d1++) {
                    for (int d2 = -1; d2 <= 1; d2++) {
                        int value = 0;

                        if (j1 == j2) value += grid[i][j1];
                        else value += grid[i][j1] + grid[i][j2];

                        if (j1+d1 >= 0 && j1+d1 < c && j2+d2 >= 0 && j2+d2 < c)
                            value += prev[j1+d1][j2+d2];
                        else 
                            value += -1e9;

                        maxi = max(maxi, value);
                    }
                } 

                curr[j1][j2] = maxi;
            }
        }

        prev = curr;
    }

    return prev[0][c-1];
}
```

## Analysis

- **Time Complexity**: `O(r * c * c) * 9`
- **Space Complexity**: `O(c * c)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/ninja-and-his-friends_3125885

## Tags

#dp #recursion #sum #maximization #grid #3d-dp

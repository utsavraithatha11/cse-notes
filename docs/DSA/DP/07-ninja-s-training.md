# 7. Ninja'S Training

## Description

- There is a N x 3 array of points.
- The ninja cannot earn points from the index which was taken in previous step.
- Find max points which ninja can earn.

## Solutions
## 1) Memorization

```cpp
int solve(int day, int last, vector<vector<int>> &points, vector<vector<int>> &dp) {
    if (day == 0) {
        int maxi = 0;
        for (int task = 0; task < 3; task++) {
            if (task != last) {
                maxi = max(maxi, points[0][task]);
            }
        }

        return maxi;
    }

    if (dp[day][last] != -1) return dp[day][last];

    int maxi = 0;

    for (int task = 0; task < 3; task++) {
        if (task != last) {
            maxi = max(maxi, points[day][task] + solve(day - 1, task, points, dp));
        }
    }

    return dp[day][last] = maxi;
}

int ninjaTraining(int n, vector<vector<int>> &points)
{
    vector<vector<int>> dp(n, vector<int> (4, -1));

    return solve(n - 1, 3, points, dp);
}
```

## Analysis

- **Time Complexity**: `O(n * 4 * 3)`
- **Space Complexity**: `O(n) + O(n * 4)`


---

## 2) Tabulation

```cpp
#include <bits/stdc++.h>

int ninjaTraining(int n, vector<vector<int>> &points)
{
    vector<vector<int>> dp(n, vector<int> (4, 0));

    dp[0][0] = max(points[0][1], points[0][2]);
    dp[0][1] = max(points[0][0], points[0][2]);
    dp[0][2] = max(points[0][0], points[0][1]);
    dp[0][3] = max({points[0][0], points[0][1], points[0][2]});

    for (int day = 1; day < n; day++) {
        for (int last = 0; last < 4; last++) {
            for (int task = 0; task < 3; task++) {
                if (task != last) {
                    int point = points[day][task] + dp[day - 1][task];
                    dp[day][last] = max(dp[day][last], point);
                }
            }
        }
    }

    return dp[n-1][3];
}
```

## Analysis

- **Time Complexity**: `O(n * 4 * 3)`
- **Space Complexity**: `O(n * 4)`


---

## 3) Space Optimization

```cpp
#include <bits/stdc++.h>

int ninjaTraining(int n, vector<vector<int>> &points)
{
    vector<int> prev(4, 0);

    prev[0] = max(points[0][1], points[0][2]);
    prev[1] = max(points[0][0], points[0][2]);
    prev[2] = max(points[0][0], points[0][1]);
    prev[3] = max({points[0][0], points[0][1], points[0][2]});

    for (int day = 1; day < n; day++) {
        vector<int> temp(4, 0);
        
        for (int last = 0; last < 4; last++) {
            for (int task = 0; task < 3; task++) {
                if (task != last) {
                    int point = points[day][task] + prev[task];
                    temp[last] = max(temp[last], point);
                }
            }
        }
        
        prev = temp;
    }

    return prev[3];
}
```

## Analysis

- **Time Complexity**: `O(n * 4 * 3)`
- **Space Complexity**: `O(4)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/ninja-s-training_3621003

## Tags

#recursion #sum #dp #maximization 
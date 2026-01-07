# 32. Distinct Subsequences

## Description

- Find no. of distinct subsequences of s which equals t

## Solutions
## 1) Memorization

```cpp
class Solution {
public:
    int solve(int i, int j, string &s, string &t, vector<vector<int>> &dp) {
        if (j == -1) return 1;

        if (i == -1) return 0;

        if (dp[i][j] != -1) return dp[i][j];

        if (s[i] == t[j]) {
            return dp[i][j] = solve(i-1, j-1, s, t, dp) + solve(i-1, j, s, t, dp);
        }

        return dp[i][j] = solve(i-1, j, s, t, dp);
    }

    int numDistinct(string s, string t) {
        int n = s.size();
        int m = t.size();
        vector<vector<int>> dp(n, vector<int> (m, -1)); 
        return solve(n-1, m-1, s, t, dp);
    }
};
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(n * m) + O(n + m)`


---

## 2) Tabulation

```cpp
class Solution {
public:

	// for reference - shifted arrays
	int solve(int i, int j, string &s, string &t, vector<vector<int>> &dp) {
        if (j == 0) return 1;

        if (i == 0) return 0;

        if (dp[i][j] != -1) return dp[i][j];

        if (s[i-1] == t[j-1]) {
            return dp[i][j] = solve(i-1, j-1, s, t, dp) + solve(i-1, j, s, t, dp);
        }

        return dp[i][j] = solve(i-1, j, s, t, dp);
    }

    int numDistinct(string s, string t) {
        int n = s.size();
        int m = t.size();
        vector<vector<unsigned long long>> dp(n+1, vector<unsigned long long> (m+1, 0));

        for (int i=0; i<=n; i++) {
            dp[i][0] = 1;
        }

        for (int i=1; i<=n; i++) {
            for (int j=1; j<=m; j++) {
                if (s[i-1] == t[j-1]) {
                    dp[i][j] = dp[i-1][j-1] + dp[i-1][j];
                } else {
                    dp[i][j] = dp[i-1][j];
                }
            }
        }

        return (int)dp[n][m];
    }
};
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(n * m)`

---

## 3) Space Optimization

```cpp
class Solution {
public:
    int numDistinct(string s, string t) {
        int n = s.size();
        int m = t.size();
        vector<vector<unsigned long long>> dp(n+1, vector<unsigned long long> (m+1, 0));
        vector<unsigned long long> prev(m+1, 0), curr(m+1, 0);

        prev[0] = curr[0] = 1;

        for (int i=1; i<=n; i++) {
            for (int j=1; j<=m; j++) {
                if (s[i-1] == t[j-1]) {
                    curr[j] = prev[j-1] + prev[j];
                } else {
                    curr[j] = prev[j];
                }
            }

            prev = curr;
        }

        return prev[m];
    }
};
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(m)`


---

## 3) Space Optimization - 1D

```cpp
class Solution {
public:
    int numDistinct(string s, string t) {
        int n = s.size();
        int m = t.size();
        vector<vector<unsigned long long>> dp(n+1, vector<unsigned long long> (m+1, 0));
        vector<unsigned long long> prev(m+1, 0);

        prev[0] = 1;

        for (int i=1; i<=n; i++) {
            for (int j=m; j>=1; j--) {
                if (s[i-1] == t[j-1]) {
                    prev[j] = prev[j-1] + prev[j];
                } else {
                    prev[j] = prev[j];
                }
            }
        }

        return prev[m];
    }
};
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(m)`


---
## Resources

- **Problem Link**: https://leetcode.com/problems/distinct-subsequences/

## Tags

#dp #recursion #strings 
# 34. Wildcard Matching

## Description

- Match string pattern with string str.
- patterns contains ? or * or letters
- * means any string (0 or more letters)
- ? means single letter

## Solutions
## 1) Memorization

```cpp
class Solution {
public:

    bool solve(int i, int j, string &s, string &p, vector<vector<int>> &dp) {
        if (i == -1 && j == -1) return true;

        if (j == -1) return false;

        if (i == -1) {
            for (int k=0; k<=j; k++) {
                if (p[k] != '*') return false;
            }

            return true;
        }

        if (dp[i][j] != -1) return dp[i][j];

        if (s[i] == p[j] || p[j] == '?') {
            return dp[i][j] = solve(i-1, j-1, s, p, dp);
        }

        if (p[j] == '*') {
            return dp[i][j] = solve(i, j-1, s, p, dp) | solve(i-1, j, s, p, dp);
        }

        return dp[i][j] = false;
    }

    bool isMatch(string s, string p) {
        int n = s.size();
        int m = p.size();

        vector<vector<int>> dp(n, vector<int> (m, -1));

        return solve(n-1, m-1, s, p, dp);
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
    bool isMatch(string s, string p) {
        int n = s.size();
        int m = p.size();

        vector<vector<bool>> dp(n+1, vector<bool> (m+1, false));

        dp[0][0] = true;

        for (int i=1; i<=n; i++) {
            dp[i][0] = false;
        }

        for (int j=1; j<=m; j++) {
            dp[0][j] = p[j-1] == '*' && dp[0][j-1];
        }

        for (int i=1; i<=n; i++) {
            for (int j=1; j<=m; j++) {
                if (s[i-1] == p[j-1] || p[j-1] == '?') {
                    dp[i][j] = dp[i-1][j-1];
                } else if (p[j-1] == '*') {
                    dp[i][j] = dp[i][j-1] | dp[i-1][j];
                } else {
                    dp[i][j] = false;
                }
            }
        }

        return dp[n][m];
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
    bool isMatch(string s, string p) {
        int n = s.size();
        int m = p.size();

        vector<bool> prev(m+1, false), curr(m+1, false);

        prev[0] = true;

        for (int j=1; j<=m; j++) {
            prev[j] = p[j-1] == '*' && prev[j-1];
        }

        for (int i=1; i<=n; i++) {
            for (int j=1; j<=m; j++) {
                if (s[i-1] == p[j-1] || p[j-1] == '?') {
                    curr[j] = prev[j-1];
                } else if (p[j-1] == '*') {
                    curr[j] = curr[j-1] | prev[j];
                } else {
                    curr[j] = false;
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

## Resources

- **Problem Link**: https://leetcode.com/problems/wildcard-matching/

## Tags

#dp #recursion #strings 
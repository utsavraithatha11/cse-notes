## Description

- Insert, Delete or replace in str1 to make it equal to str2
- Return min operations

## Solutions
## 1) Memorization

```cpp
class Solution {
public:
    int solve(int i, int j, string &word1, string &word2, vector<vector<int>> &dp) {
        if (j == -1) return i + 1;

        if (i == -1) return j + 1;

        if (dp[i][j] != -1) return dp[i][j];

        if (word1[i] == word2[j]) return dp[i][j] = solve(i-1, j-1, word1, word2, dp);

        return dp[i][j] = 1 + min({
            solve(i-1, j-1, word1, word2, dp), 
            solve(i, j-1, word1, word2, dp), 
            solve(i-1, j, word1, word2, dp)
        });
    }

    int minDistance(string word1, string word2) {
        int n = word1.size();
        int m = word2.size();

        vector<vector<int>> dp(n, vector<int> (m, -1));

        return solve(n-1, m-1, word1, word2, dp);
    }
};
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(n * m) + O(n+m)`


---

## 2) Tabulation

```cpp
class Solution {
public:
    int solve(int i, int j, string &word1, string &word2, vector<vector<int>> &dp) {
        if (j == 0) return i;

        if (i == 0) return j;

        if (dp[i][j] != -1) return dp[i][j];

        if (word1[i-1] == word2[j-1]) return dp[i][j] = solve(i-1, j-1, word1, word2, dp);

        return dp[i][j] = 1 + min({
            solve(i-1, j-1, word1, word2, dp), 
            solve(i, j-1, word1, word2, dp), 
            solve(i-1, j, word1, word2, dp)
        });
    }

    int minDistance(string word1, string word2) {
        int n = word1.size();
        int m = word2.size();

        vector<vector<int>> dp(n+1, vector<int> (m+1, 0));

        for (int i=0; i<=n; i++) {
            dp[i][0] = i;
        }

        for (int j=0; j<=m; j++) {
            dp[0][j] = j;
        }

        for (int i=1; i<=n; i++) {
            for (int j=1; j<=m; j++) {
                if (word1[i-1] == word2[j-1]) {
                    dp[i][j] = dp[i-1][j-1];
                }
                else {
                    dp[i][j] = 1 + min({dp[i-1][j-1], dp[i][j-1], dp[i-1][j]});
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
    int minDistance(string word1, string word2) {
        int n = word1.size();
        int m = word2.size();

        vector<int> prev(m+1, 0), curr(m+1, 0);

        for (int i=0; i<=m; i++) {
            prev[i] = i;
        }

        for (int i=1; i<=n; i++) {
            curr[0] = i;
            for (int j=1; j<=m; j++) {
                if (word1[i-1] == word2[j-1]) {
                    curr[j] = prev[j-1];
                }
                else {
                    curr[j] = 1 + min({prev[j-1], curr[j-1], prev[j]});
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

- **Problem Link**: https://leetcode.com/problems/edit-distance/

## Tags

#dp #recursion #strings 
## Solutions
## 1) Memorization

```cpp
#include <bits/stdc++.h>

int solve(int i, int j, string &s, string &t, vector<vector<int>> &dp) {
	if (i == -1 || j == -1) {
		return 0;
	}

	if (dp[i][j] != -1) return dp[i][j];

	if (s[i] == t[j]) return dp[i][j] = 1 + solve(i-1, j-1, s, t, dp);

	return dp[i][j] = max(solve(i-1, j, s, t, dp), solve(i, j-1, s, t, dp));
}

int lcs(string s, string t) {
	int n = s.size();
	int m = t.size();

	vector<vector<int>> dp(n, vector<int> (m, -1));
	return solve(n-1, m-1, s, t, dp);
}
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(n * m) + O(n + m)`

## Notes

- Match-NotMatch technique
- Check if it matches on index
- Else take optimized of reduced index by 1 differently

---

## 2) Tabulation

- Uses shifted DP, because -1 index base case is not possible.

```cpp
#include <bits/stdc++.h>

int solve(int i, int j, string &s, string &t, vector<vector<int>> &dp) {
	if (i == 0 || j == 0) {
		return 0;
	}

	if (dp[i][j] != -1) return dp[i][j];

	if (s[i-1] == t[j-1]) return dp[i][j] = 1 + solve(i-1, j-1, s, t, dp);

	return dp[i][j] = max(solve(i-1, j, s, t, dp), solve(i, j-1, s, t, dp));
}


int lcs(string s, string t) {
	int n = s.size();
	int m = t.size();

	vector<vector<int>> dp(n+1, vector<int> (m+1, 0));

	for (int i=0; i<=n; i++) {
		dp[i][0] = 0;
	}

	for (int i=0; i<=m; i++) {
		dp[0][i] = 0;
	}

	for (int i=1; i<=n; i++) {
		for (int j=1; j<=m; j++) {
			if (s[i-1] == t[j-1]) {
				dp[i][j] = 1 + dp[i-1][j-1];
			} else {
				dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
			}
		}
	}

	return dp[n][m];
}
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(n * m)`

---

## 3) Space Optimization

```cpp
#include <bits/stdc++.h>

int lcs(string s, string t) {
	int n = s.size();
	int m = t.size();

	vector<int> prev(m+1, 0), curr(m+1, 0);

	for (int i=0; i<m; i++) {
		prev[i] = 0;
	}

	for (int i=1; i<=n; i++) {
		for (int j=1; j<=m; j++) {
			if (s[i-1] == t[j-1]) {
				curr[j] = 1 + prev[j-1];
			} else {
				curr[j] = max(prev[j], curr[j-1]);
			}
		}

		prev = curr;
	}

	return prev[m];
}
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(m)`

---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/longest-common-subsequence_624879

## Tags

#dp #recursion #lcs #match-notMatch #strings

## Description

- Count all unique paths on m x n grid by going only down and right.

## Solutions
## 1) Memorization

```cpp
#include <bits/stdc++.h>
int solve(int i, int j, vector<vector<int>> &dp) {
	if (i == 0 && j == 0) return 1;

	if (i < 0 || j < 0) return 0;

	if (dp[i][j] != -1) return dp[i][j];

	int up = solve(i-1, j, dp);
	int left = solve(i, j-1, dp);

	return dp[i][j] = up + left;
} 

int uniquePaths(int m, int n) {
	vector<vector<int>> dp(m, vector<int> (n, -1));

	return solve(m-1, n-1, dp);
}
```

## Analysis

- **Time Complexity**: `O(m * n)`
- **Space Complexity**: `O(path length) + O(m * n) = O(m - 1 + n - 1) + O(m * n)`


---

## 2) Tabulation

```cpp
#include <bits/stdc++.h>

int uniquePaths(int m, int n) {
	vector<vector<int>> dp(m, vector<int> (n, 0));
	dp[0][0] = 1;

	for (int i=0; i<m; i++) {
		for (int j=0; j<n; j++) {
			if (i == 0 && j == 0) dp[i][j] = 1;
			else {
				int up = 0, left = 0;
				if (i > 0) up = dp[i-1][j];
				if (j > 0) left = dp[i][j-1];
				dp[i][j] = up + left;
			}
		}
	}

	return dp[m-1][n-1];
}
```

## Analysis

- **Time Complexity**: `O(m * n)`
- **Space Complexity**: `O(m * n) `


---

## 3) Space Optimization

```cpp
#include <bits/stdc++.h>

int uniquePaths(int m, int n) {
	vector<int> prev_row(n);
	prev_row[0] = 1;

	for (int i=0; i<m; i++) {
		vector<int> row(n);
		for (int j=0; j<n; j++) {
			if (i == 0 && j == 0) row[j] = 1;
			else {
				int up = 0, left = 0;
				if (i > 0) up = prev_row[j];
				if (j > 0) left = row[j-1];
				row[j] = up + left;
			}
		}

		prev_row = row;
	}

	return prev_row[n-1];
}
```

## Analysis

- **Time Complexity**: `O(m * n)`
- **Space Complexity**: `O(n)`

## Notes

- Answer is (m + n - 2) C (m - 1).

![[Pasted image 20250323133732.png]]

```cpp
#include <bits/stdc++.h>

int uniquePaths(int m, int n) {
	int N = m + n - 2;
	int r = m - 1;
	double res = 1;

	for (int i=1; i<=r; i++) {
		res = (res * (N - r + i)) / i;
	}

	return int(res);
}
```

## Analysis

- **Time Complexity**: `O(m)`
- **Space Complexity**: `O(1)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/total-unique-paths_1081470

## Tags

#dp #recursion #count #grid 
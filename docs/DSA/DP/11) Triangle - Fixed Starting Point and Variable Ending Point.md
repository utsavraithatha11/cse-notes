## Description

- Minimize path sum by going only down or right diagonal.

## Solutions
## 1) Memorization

```cpp
#include <bits/stdc++.h>

int solve(int i, int j, int &n, vector<vector<int>> &triangle, vector<vector<int>> &dp) {
	if (i == n-1) return triangle[i][j];

	if (dp[i][j] != -1) return dp[i][j];

	int down = triangle[i][j] + solve(i+1, j, n, triangle, dp);
	int diagonal = triangle[i][j] + solve(i+1, j+1, n, triangle, dp);

	return dp[i][j] = min(down, diagonal);
}

int minimumPathSum(vector<vector<int>>& triangle, int n){
	vector<vector<int>> dp(n, vector<int> (n, -1));
	return solve(0, 0, n, triangle, dp);
}
```

## Analysis

- **Time Complexity**: `O(n * n)`
- **Space Complexity**: `O(n) + O(n * n)`


---

## 2) Tabulation

```cpp
#include <bits/stdc++.h>

int minimumPathSum(vector<vector<int>>& triangle, int n){
	vector<vector<int>> dp(n, vector<int> (n, 0));

	// base case
	for (int j=0; j<n; j++) {
		dp[n-1][j] = triangle[n-1][j];
	}

	for (int i=n-2; i>=0; i--) {
		for (int j=i; j>=0; j--) {
			int down = triangle[i][j] + dp[i+1][j];
			int diagonal = triangle[i][j] + dp[i+1][j+1];

			dp[i][j] = min(down, diagonal);
		}
	}

	return dp[0][0];
}
```

## Analysis

- **Time Complexity**: `O(n * n)`
- **Space Complexity**: `O(n * n)`

---

## 3) Space Optimization

```cpp
#include <bits/stdc++.h>

int minimumPathSum(vector<vector<int>>& triangle, int n){
	vector<int> prev_row(n, 0);

	// base case
	for (int j=0; j<n; j++) {
		prev_row[j] = triangle[n-1][j];
	}

	for (int i=n-2; i>=0; i--) {
		vector<int> row(n, 0);
		for (int j=i; j>=0; j--) {
			int down = triangle[i][j] + prev_row[j];
			int diagonal = triangle[i][j] + prev_row[j+1];

			row[j] = min(down, diagonal);
		}

		prev_row = row;
	}

	return prev_row[0];
}
```

## Analysis

- **Time Complexity**: `O(n * n)`
- **Space Complexity**: `O(n)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/triangle_1229398

## Tags

#dp #recursion #sum #minimization #grid 
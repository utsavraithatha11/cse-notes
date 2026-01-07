# 9. Grid Unique Paths 2

## Description

- Here there will be dead cells (-1).

## Solutions
## 1) Memorization

```cpp
int mod = 1e9 + 7;

int solve(int i, int j, vector<vector<int>> &dp, vector<vector<int>> &mat) {
	if (i == 0 && j == 0) return 1;

	if (i < 0 || j < 0) return 0;

    if (mat[i][j] == -1) return 0;

	if (dp[i][j] != -1) return dp[i][j];

	int up = solve(i-1, j, dp, mat);
	int left = solve(i, j-1, dp, mat);

	return dp[i][j] = (up + left) % mod;
} 

int mazeObstacles(int n, int m, vector< vector< int> > &mat) {
    vector<vector<int>> dp(n, vector<int> (m, -1));

	return solve(n-1, m-1, dp, mat);
}
```

## Analysis

- **Time Complexity**: `O(m * n)`
- **Space Complexity**: `O(path length) + O(m * n) = O(m - 1 + n - 1) + O(m * n)`

---

## 2) Tabulation

```cpp
int mod = 1e9 + 7;

int mazeObstacles(int n, int m, vector< vector< int> > &mat) {
    vector<vector<int>> dp(n, vector<int> (m, 0));
	dp[0][0] = 1;

	for (int i=0; i<n; i++) {
		for (int j=0; j<m; j++) {
            if (mat[i][j] == -1) dp[i][j] = 0;
			else if(i == 0 && j == 0) dp[i][j] = 1;
			else {
				int up = 0, left = 0;
				if (i > 0) up = dp[i-1][j];
				if (j > 0) left = dp[i][j-1];
				dp[i][j] = (up + left) % mod;
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
int mod = 1e9 + 7;

int mazeObstacles(int n, int m, vector< vector< int> > &mat) {
    vector<int> prev_row(n);
	prev_row[0] = 1;

	for (int i=0; i<n; i++) {
		vector<int> row(m);
        for (int j=0; j<m; j++) {
            if (mat[i][j] == -1) row[j] = 0;
			else if(i == 0 && j == 0) row[j] = 1;
			else {
				int up = 0, left = 0;
				if (i > 0) up = prev_row[j];
				if (j > 0) left = row[j-1];
				row[j] = (up + left) % mod;
			}
		}

        prev_row = row;
	}

	return prev_row[m-1];
}
```

## Analysis

- **Time Complexity**: `O(m * n)`
- **Space Complexity**: `O(n)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/unique-paths-ii_977241

## Tags

#dp #recursion #count #grid 
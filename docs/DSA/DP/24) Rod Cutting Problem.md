## Description

- Cut the rod into pieces maximizing the profit.

## Solutions
## 1) Memorization

```cpp
int solve(int ind, int remRod, vector<int> &price, vector<vector<int>> &dp) {
	if (ind == 0) {
		return price[0] * remRod;
	}

	if (dp[ind][remRod] != -1) return dp[ind][remRod];

	int notTake = solve(ind-1, remRod, price, dp);

	int take = 0;
	if (remRod >= ind+1) {
		take = price[ind] + solve(ind, remRod - ind - 1, price, dp);
	}

	return dp[ind][remRod] = max(take, notTake);
}

int cutRod(vector<int> &price, int n)
{
	// Write your code here.
	vector<vector<int>> dp(n, vector<int> (n+1, -1));

	return solve(n-1, n, price, dp);
}
```

## Analysis

- **Time Complexity**: `O(n * n)`
- **Space Complexity**: `O(n * n) + O(n)`


---

## 2) Tabulation

```cpp
int cutRod(vector<int> &price, int n)
{
	// Write your code here.
	vector<vector<int>> dp(n, vector<int> (n+1, 0));

	for (int remRod=0; remRod<=n; remRod++) {
		dp[0][remRod] = price[0] * remRod;
	}

	for (int ind=1; ind<n; ind++) {
		for (int remRod=0; remRod<=n; remRod++) {
			int notTake = dp[ind-1][remRod];

			int take = 0;
			if (remRod >= ind+1) {
				take = price[ind] + dp[ind][remRod - ind - 1];
			}

			dp[ind][remRod] = max(take, notTake);
		}
	}

	return dp[n-1][n];
}
```

## Analysis

- **Time Complexity**: `O(n * n)`
- **Space Complexity**: `O(n * n)`

---

## 3) Space Optimization

```cpp
int cutRod(vector<int> &price, int n)
{
	// Write your code here.
	vector<int> curr(n+1, 0), prev(n+1, 0);

	for (int remRod=0; remRod<=n; remRod++) {
		prev[remRod] = price[0] * remRod;
	}

	for (int ind=1; ind<n; ind++) {
		for (int remRod=0; remRod<=n; remRod++) {
			int notTake = prev[remRod];

			int take = 0;
			if (remRod >= ind+1) {
				take = price[ind] + curr[remRod - ind - 1];
			}

			curr[remRod] = max(take, notTake);
		}

		prev = curr;
	}

	return prev[n];
}
```

## Analysis

- **Time Complexity**: `O(n * n)`
- **Space Complexity**: `O(n)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/rod-cutting-problem_800284

## Tags

#dp #recursion #take-not-take #maximization 
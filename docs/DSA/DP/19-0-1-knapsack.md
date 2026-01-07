# 19. 0 1 Knapsack

## Solutions
## 1) Memorization

```cpp
#include <bits/stdc++.h> 

int solve(int ind, int wt, vector<int> &weight, vector<int> &value, vector<vector<int>> &dp) {
	if (ind == 0) {
		if (weight[0] <= wt) return value[0];
		return 0;
	}

	if (dp[ind][wt] != -1) return dp[ind][wt];

	int notTake = solve(ind-1, wt, weight, value, dp);
	int take = 0;
	if (weight[ind] <= wt) take = value[ind] + solve(ind-1, wt-weight[ind], weight, value, dp);

	return dp[ind][wt] = max(take, notTake);
}

int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) {
	vector<vector<int>> dp(n, vector<int> (maxWeight+1, -1));

	return solve(n-1, maxWeight, weight, value, dp);
}
```

## Analysis

- **Time Complexity**: `O(n * wt)`
- **Space Complexity**: `O(n * wt) + O(n)`


---

## 2) Tabulation

```cpp
#include <bits/stdc++.h> 

int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) {
	vector<vector<int>> dp(n, vector<int> (maxWeight+1, 0));

	// base case
	for (int i=weight[0]; i<=maxWeight; i++) dp[0][i] = value[0];

	for (int i=1; i<n; i++) {
		for (int wt=0; wt<=maxWeight; wt++) {
			int notTake = dp[i-1][wt];
			int take = 0;
			if (weight[i] <= wt) take = value[i] + dp[i-1][wt-weight[i]];

			dp[i][wt] = max(take, notTake);
		}
	}

	return dp[n-1][maxWeight];
}
```

## Analysis

- **Time Complexity**: `O(n * wt)`
- **Space Complexity**: `O(n * wt)`


---

## 3) Space Optimization

```cpp
#include <bits/stdc++.h> 

int knapsack(vector<int> weight, vector<int> value, int n, int maxWeight) {
	vector<int> prev(maxWeight + 1, 0); // using maxWeight --> 0, no need of curr

	// base case
	for (int i=weight[0]; i<=maxWeight; i++) prev[i] = value[0];

	for (int i=1; i<n; i++) {
		for (int wt=maxWeight; wt>=0; wt--) {
			int notTake = prev[wt];
			int take = 0;
			if (weight[i] <= wt) take = value[i] + prev[wt-weight[i]];

			prev[wt] = max(take, notTake);
		}
	}

	return prev[maxWeight];
}
```

## Analysis

- **Time Complexity**: `O(n * wt)`
- **Space Complexity**: `O(wt)`

---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/0-1-knapsack_920542

## Tags

#dp #recursion #knapsack #maximization

## Solutions
## 1) Memorization

```cpp
int mod = (int)1e9 + 7;

int solve(int ind, int sum, vector<int> &arr, vector<vector<int>> &dp) {
    
    if (ind == 0) {
		if (sum == 0) {
			if (arr[0] == 0) return 2;
			return 1;
		}

		return (arr[0] == sum);
	}

	if (dp[ind][sum] != -1) return dp[ind][sum];

	int notPick = solve(ind-1, sum, arr, dp);
	int pick = 0;
	if (arr[ind] <= sum) 
		pick = solve(ind-1, sum-arr[ind], arr, dp);

	return dp[ind][sum] = (pick + notPick) % mod;
}

int findWays(vector<int>& arr, int k) {
	int n = arr.size();
	vector<vector<int>> dp(n, vector<int> (k+1, -1));

	return solve(n-1, k, arr, dp);
}

```

## Analysis

- **Time Complexity**: `O(n * k)`
- **Space Complexity**: `O(n * k) + O(n)`


---

## 2) Tabulation

```cpp
int mod = (int)1e9 + 7;

int findWays(vector<int>& arr, int k) {
	int n = arr.size();
	vector<vector<int>> dp(n, vector<int> (k+1, 0));

	if (arr[0] == 0) dp[0][0] = 2;
	else dp[0][0] = 1;

	if (arr[0] != 0 && arr[0] <= k) dp[0][arr[0]] = 1;

	for (int i=1; i<n; i++) {
		for (int sum = 0; sum <= k; sum++) {
			int notPick = dp[i-1][sum];
			int pick = 0;
			if (arr[i] <= sum) 
				pick = dp[i-1][sum-arr[i]];

			dp[i][sum] = (pick + notPick) % mod;
		}
	}

	return dp[n-1][k];
}

```

## Analysis

- **Time Complexity**: `O(n * k)`
- **Space Complexity**: `O(n * k)


---

## 3) Space Optimization

```cpp
int mod = (int)1e9 + 7;

int findWays(vector<int>& arr, int k) {
	int n = arr.size();
	vector<vector<int>> dp(n, vector<int> (k+1, 0));
	vector<int> prev(k+1, 0), curr(k+1, 0);

	if (arr[0] == 0) prev[0] = 2;
	else prev[0] = 1;

	if (arr[0] != 0 && arr[0] <= k) prev[arr[0]] = 1;

	for (int i=1; i<n; i++) {
		for (int sum = 0; sum <= k; sum++) {
			int notPick = prev[sum];
			int pick = 0;
			if (arr[i] <= sum) 
				pick = prev[sum-arr[i]];

			curr[sum] = (pick + notPick) % mod;
		}

		prev = curr;
	}

	return prev[k];
}

```

## Analysis

- **Time Complexity**: `O(n * k)`
- **Space Complexity**: `O(k)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/number-of-subsets_3952532

## Tags

#dp #recursion #count #subset #subset-sum #subsequence 
## Description

- Minor change in LCS - If not match, it is 0.
- Return max len in the DP Table

## Solutions

## 1) Tabulation

```cpp
int lcs(string &s, string &t){
    int n = s.size();
	int m = t.size();

	vector<vector<int>> dp(n+1, vector<int> (m+1, 0));

	for (int i=0; i<=n; i++) {
		dp[i][0] = 0;
	}

	for (int i=0; i<=m; i++) {
		dp[0][i] = 0;
	}

    int ans = 0;

	for (int i=1; i<=n; i++) {
		for (int j=1; j<=m; j++) {
			if (s[i-1] == t[j-1]) {
				dp[i][j] = 1 + dp[i-1][j-1];
                ans = max(ans, dp[i][j]);
			} else {
				dp[i][j] = 0;
			}
		}
	}

    return ans;
}
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(n * m)`

## Notes



---

## 2) Space Optimization

```cpp
int lcs(string &s, string &t){
    int n = s.size();
	int m = t.size();

	vector<int> prev(m+1, 0), curr(m+1, 0);

    int ans = 0;

	for (int i=1; i<=n; i++) {
		for (int j=1; j<=m; j++) {
			if (s[i-1] == t[j-1]) {
				curr[j] = 1 + prev[j-1];
                ans = max(ans, curr[j]);
			} else {
				curr[j] = 0;
			}
		}

		prev = curr;
	}

    return ans;
}
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(m)`

## Notes

![[Pasted image 20260102194358.png]]

---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/longest-common-substring_1235207

## Tags

#dp #recursion #lcs #match-notMatch #strings 
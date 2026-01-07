## Description

- Use DP table of max LCS to solve this.

## Solution

```cpp
#include<bits/stdc++.h>

string findLCS(int n, int m, string &s, string &t){
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

	string ans = "";
	int ansLen = dp[n][m];
	for (int i=0; i<ansLen; i++) ans += '$';

	int ind = ansLen-1, i = n, j = m;

	while (i > 0 && j > 0) {
		if (s[i-1] == t[j-1]) {
			ans[ind--] = s[i-1];
			i--;
			j--;
		}
		else if (dp[i][j-1] >= dp[i-1][j]) {
			j--;
		} 
		else {
			i--;
		}
	}

	return ans;
}
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(n * m)`

## Notes

![[Pasted image 20260102191619.png]]

---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/print-longest-common-subsequence_8416383

## Tags

#dp #recursion #match-notMatch #strings #lcs 
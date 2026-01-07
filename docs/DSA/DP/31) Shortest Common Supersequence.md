## Description

- `n + m - lcs(s, t)`
- Construct string from DP table

## Solutions

## 1) Tabulation

```cpp
#include <bits/stdc++.h> 
string shortestSupersequence(string s, string t)
{
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

	string ans = "";

	int i = n, j = m;

	while (i > 0 && j > 0) {
		if (s[i-1] == t[j-1]) {
			ans += s[i-1];
			i--;
			j--;
		}
		else if (dp[i][j-1] >= dp[i-1][j]) {
			ans += t[j-1];
			j--;
		} 
		else {
			ans += s[i-1];
			i--;
		}
	}

	while (i > 0) {
		ans += s[i-1];
		i--;
	}


	while (j > 0) {
		ans += t[j-1];
		j--;
	}

	reverse(ans.begin(), ans.end());

	return ans;
}
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(m)`

## Notes

![[Pasted image 20260102205908.png]]
![[Pasted image 20260102205932.png]]

---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/shortest-supersequence_4244493

## Tags

#dp #recursion #match-notMatch #strings #lcs 
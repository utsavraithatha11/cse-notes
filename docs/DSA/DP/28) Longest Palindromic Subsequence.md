## Description

- `lcs(s, rev(s))` is answer

## Solutions

## 1) Space Optimization

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

int longestPalindromeSubsequence(string s)
{
	string rev = s;
	reverse(rev.begin(), rev.end());

	return lcs(s, rev);
}
```

## Analysis

- **Time Complexity**: `O(n * n)`
- **Space Complexity**: `O(n)`

---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/longest-palindromic-subsequence_842787

## Tags

#dp #recursion #lcs #match-notMatch #strings 
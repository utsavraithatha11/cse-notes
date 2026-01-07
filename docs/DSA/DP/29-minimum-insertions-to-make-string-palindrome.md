# 29. Minimum Insertions To Make String Palindrome

## Description

- `len(s) - lps(s)`

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

int minimumInsertions(string &str)
{
	return str.size() - longestPalindromeSubsequence(str);
}

```

## Analysis

- **Time Complexity**: `O(n * n)`
- **Space Complexity**: `O(n)`

---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/minimum-insertions-to-make-a-string-palindrome_985293

## Tags

#dp #recursion #match-notMatch #strings #lcs 
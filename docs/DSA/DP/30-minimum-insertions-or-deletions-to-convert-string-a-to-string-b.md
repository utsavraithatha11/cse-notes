# 30. Minimum Insertions Or Deletions To Convert String A To String B

## Description

`int deletions = s1.size() - lcs(s1, s2);
`int insertions = s2.size() - lcs(s1, s2);`
`return deletions + insertions;

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


int canYouMake(string &s1, string &s2){
    int deletions = s1.size() - lcs(s1, s2);
    int insertions = s2.size() - lcs(s1, s2);

    return deletions + insertions;
}
```

## Analysis

- **Time Complexity**: `O(n * m)`
- **Space Complexity**: `O(m)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/minimum-number-of-deletions-and-insertions_4244510

## Tags

#dp #recursion #match-notMatch #strings #lcs 
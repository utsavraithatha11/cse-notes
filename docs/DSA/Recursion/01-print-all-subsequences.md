# 1. Print All Subsequences

	
## Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

#ifndef ONLINE_JUDGE
#include "debug.h"
#else
#define dbg(x...)
#endif

#define ll long long
#define pb push_back

void subseq(int ind, vector<int> &a, vector<int> &ds) {
    if (ind == a.size()) {
        for (auto num : ds) {
            cout << num << " ";
        }
        
        if (ds.size() == 0) {
            cout << "{}";
        }

        cout << endl;
        return;
    };

    // take
    ds.push_back(a[ind]);
    subseq(ind + 1, a, ds);
    ds.pop_back();

    // not-take
    subseq(ind + 1, a, ds);
}

void solve() {
    int n;
    cin >> n;

    vector<int> a(n);   

    for (int i=0; i<n; i++) cin >> a[i];

    vector<int> ds;

    subseq(0, a, ds);
}

int main() {
    solve();

    return 0;
}
```

## Analysis

- **Time Complexity**: `O(2^n * n)` 
	- 2^n for all subseq
	-  n for printing
- **Space Complexity**: `O(n)`

## Tags

#recursion #take-not-take #subsequence 
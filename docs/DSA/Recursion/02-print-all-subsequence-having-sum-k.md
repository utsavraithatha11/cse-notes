# 2. Print All Subsequence Having Sum K

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

void sum_K(int ind, vector<int> &ds, vector<int> &a, int &sum, int k) {
    if (ind == a.size()) {
        if (sum == k) {
            for (auto num : ds) {
                cout << num << " ";
            }
            cout << endl;
        }
        return;
    }

    // take
    ds.push_back(a[ind]);
    sum += a[ind];
    sum_K(ind + 1, ds, a, sum, k);
    ds.pop_back();
    sum -= a[ind];
    
    // not-take
    sum_K(ind + 1, ds, a, sum, k);
}

void solve() {
    int n, k;
    cin >> n >> k;
    
    vector<int> a(n);
    for (int i=0; i<n; i++) cin >> a[i];

    vector<int> ds;
    int sum = 0;
    sum_K(0, ds, a, sum, k);
}

int main() {
    solve();

    return 0;
}
```

## Analysis

- **Time Complexity**: `O(2^n * n)`
	- 2^n for all subseq
	- n for printing
- **Space Complexity**: `O(n)`

## Tags

#recursion #take-not-take #subsequence #sum-k

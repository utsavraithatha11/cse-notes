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

bool sum_K(int ind, vector<int> &ds, vector<int> &a, int &sum, int k) {
    if (ind == a.size()) {
        // condition - satisfied
        if (sum == k) {
            for (auto num : ds) {
                cout << num << " ";
            }
            cout << endl;
            return true;
        }

        // condition - not satisfied
        return false;
    }

    // take
    ds.push_back(a[ind]);
    sum += a[ind];
    
    if (sum_K(ind + 1, ds, a, sum, k) == true) {
        return true;
    }

    ds.pop_back();
    sum -= a[ind];
    
    // not-take
    if (sum_K(ind + 1, ds, a, sum, k) == true) {
        return true;
    }

    return false;
}

void solve() {
    int n, k;
    cin >> n >> k;
    
    vector<int> a(n);
    for (int i=0; i<n; i++) cin >> a[i];

    vector<int> ds;
    int sum = 0;
    
    if (!sum_K(0, ds, a, sum, k)) {
        cout << "No subsequence";
    }
}

int main() {
    solve();

    return 0;
}
```

## Analysis

- **Time Complexity**: `O(2^n)`
- **Space Complexity**: `O(n)`

## Tags

#recursion #sum-k #subsequence #take-not-take #only-one 
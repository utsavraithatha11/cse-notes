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

int sum_K(int ind, vector<int> &a, int &sum, int k) {
    if (ind == a.size()) {
        // condition - satisfied
        if (sum == k) {
            return 1;
        }

        // condition - not satisfied
        return 0;
    }

    // take
    sum += a[ind];
    
    int l = sum_K(ind + 1, a, sum, k);

    sum -= a[ind];
    
    // not-take
    int r = sum_K(ind + 1, a, sum, k);

    return l + r;
}

void solve() {
    int n, k;
    cin >> n >> k;
    
    vector<int> a(n);
    for (int i=0; i<n; i++) cin >> a[i];

    int sum = 0;

    cout << sum_K(0, a, sum, k);
}

int main() {
    solve();

    return 0;
}
```

## Analysis

- **Time Complexity**: `O(2^n)`
- **Space Complexity**: `O(n)`

## Notes

![[Pasted image 20250315195148.png]]
## Tags

#recursion #subsequence #sum-k #take-not-take #count

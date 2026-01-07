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

int partition(vector<int> &a, int low, int high) {
    int pivot = a[low];

    int i = low, j = high;

    while (i < j) {
        while (a[i] <= pivot && i <= high - 1) {
            i++;
        }

        while (a[j] > pivot && j >= low + 1) {
            j--;
        }

        if (i < j) {
            swap(a[i], a[j]);
        }
    }

    swap(a[low], a[j]);

    return j;
}

void quickSort(vector<int> &a, int low, int high) {
    if (low >= high) return;

    int pivot = partition(a, low, high);
    // left
    quickSort(a, low, pivot - 1);

    // right
    quickSort(a, pivot + 1, high);
}

void solve() {
    int n;
    cin >> n;
    
    vector<int> a(n);
    for (int i=0; i<n; i++) cin >> a[i];

    quickSort(a, 0, n - 1);

    for (int i=0; i<n; i++) cout << a[i] << " ";

    cout << endl;
}

int main() {
    solve();

    return 0;
}
```

## Analysis

- **Time Complexity**: `O(nlogn)`
- **Space Complexity**: `O(1)`

## Tags

#recursion #quick-sort #sorting #algorithm #divide-and-conquer 
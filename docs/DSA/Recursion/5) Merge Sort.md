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

void merge(vector<int> &a, int low, int mid, int high) {
    vector<int> temp;
    
    int left = low;
    int right = mid + 1;

    while (left <= mid && right <= high) {
        if (a[left] <= a[right]) {
            temp.push_back(a[left]);
            left++;
        } 
        else {
            temp.push_back(a[right]);
            right++;
        }
    }

    while (left <= mid) {
        temp.push_back(a[left]);
        left++;
    }

    while (right <= high) {
        temp.push_back(a[right]);
        right++;
    }

    for (int i=low; i<=high; i++) {
        a[i] = temp[i - low];
    }
}

void mergeSort(vector<int> &a, int low, int high) {
    
    // base-condition
    if (low >= high) return;

    int mid = (low + high) / 2;

    // left
    mergeSort(a, low, mid);
    // right
    mergeSort(a, mid + 1, high);

    // merge
    merge(a, low, mid, high);
}

void solve() {
    int n;
    cin >> n;
    
    vector<int> a(n);
    for (int i=0; i<n; i++) cin >> a[i];

    mergeSort(a, 0, n - 1);

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
	- n for merge at each level
	- logn for the levels of tree
- **Space Complexity**: `O(n)`

## Tags

#recursion #merge-sort #sorting #divide-and-conquer #algorithm
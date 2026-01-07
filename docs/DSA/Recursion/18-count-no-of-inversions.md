# 18. Count No. Of Inversions

## Description

- count pairs (i, j) where i < j and a[i] > a[j]

## Solution (merge sort)

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

int merge(vector<int> &a, int low, int mid, int high) {
    int cnt = 0;
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
            cnt += (mid - left + 1);
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

    return cnt;
}

int mergeSort(vector<int> &a, int low, int high) {
    int cnt = 0;

    // base-condition
    if (low >= high) return cnt;

    int mid = (low + high) / 2;

    // left
    cnt += mergeSort(a, low, mid);
    // right
    cnt += mergeSort(a, mid + 1, high);

    // merge
    cnt += merge(a, low, mid, high);

    return cnt;
}

void solve() {
    int n;
    cin >> n;
    
    vector<int> a(n);
    for (int i=0; i<n; i++) cin >> a[i];

    cout << mergeSort(a, 0, n - 1);
}

int main() {
    solve();

    return 0;
}
```

## Analysis

- **Time Complexity**: `O(nlogn)`
- **Space Complexity**: `O(n)`

## Resources

- **Problem Link**: 
## Tags

#recursion #merge-sort #count #inversions

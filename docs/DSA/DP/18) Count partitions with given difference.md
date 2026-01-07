## Description

- S1 - S2 = D and S1 >= S2
- Therefore, totSum - 2*S2 = D => S2 = (totSum - D) / 2

## Space Optimization

```cpp
#include <bits/stdc++.h> 

int mod = (int)(1e9 + 7);

int findWays(vector<int> &arr, int tar) {
    int n = arr.size();

    vector<int> prev(tar + 1, 0), curr(tar + 1, 0);

    if (arr[0] <= tar) prev[arr[0]] = 1;
    
    if (arr[0] == 0) prev[0] = 2;
    else prev[0] = 1;

    for (int i=1; i<n; i++) {
        for (int sum=0; sum<=tar; sum++) {
            int notTake = prev[sum];
            int take = 0;
            if (arr[i] <= sum) take = prev[sum-arr[i]];

            curr[sum] = (take + notTake) % mod;
        }

        prev = curr;
    }

    return prev[tar];
}

int countPartitions(int n, int d, vector<int> &arr) {
    int totSum = 0;

    for (int i=0; i<n; i++) totSum += arr[i];

    if ((totSum - d) % 2 || (totSum - d) < 0) return 0;

    int tar = (totSum - d) / 2;

    return findWays(arr, tar);
}

```

## Analysis

- **Time Complexity**: `O(n * tar)`
- **Space Complexity**: `O(tar)`

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/partitions-with-given-difference_3751628

## Tags

#dp #recursion #sum #subset-sum #subsequence 
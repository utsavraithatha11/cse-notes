# 6. House Robber 2

## Description

- Same as 5th question but a circular array

## Solution

## Space Optimization

```cpp
#include <bits/stdc++.h> 

int maximumNonAdjacentSum(vector<int> &nums){
    int n = nums.size();
    int prev2 = 0, prev = nums[0];
    int curr;

    for (int i=1; i<n; i++) {
        int take = nums[i];
        if (i > 1) take += prev2;

        int notTake = prev;

        curr = max(take, notTake);
        prev2 = prev;
        prev = curr;
    }

    return prev;
}

long long int houseRobber(vector<int>& valueInHouse)
{
    int n = valueInHouse.size();
    vector<int> temp1, temp2;

    if (n == 1) return valueInHouse[0];

    for (int i=0; i<n; i++) {
        if (i != 0) temp1.push_back(valueInHouse[i]);
        if (i != n-1) temp2.push_back(valueInHouse[i]);
    }

    return max(maximumNonAdjacentSum(temp1), maximumNonAdjacentSum(temp2));
}
```

## Analysis

- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(1)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/house-robber_839733

## Tags

#recursion #dp #sum #circular-array #take-not-take 
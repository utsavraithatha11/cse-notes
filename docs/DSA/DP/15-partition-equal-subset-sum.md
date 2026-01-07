# 15. Partition Equal Subset Sum

## Description

- Use 14th question logic.

## Space Optimization

```cpp
bool subsetSumToK(int n, int k, vector<int> &arr) {
    vector<bool> prev(k+1, 0), curr(k+1, 0);

    // base cases
    prev[0] = true;
    if (arr[0] <= k) prev[arr[0]] = true;
    curr[0] = true;

    for (int i=1; i<n; i++) {
        for (int target = 1; target <= k; target++) {
            bool notTake = prev[target];
            bool take = false;
            if (target >= arr[i]) take = prev[target-arr[i]];

            curr[target] = take | notTake;
        }

        prev = curr;
    }

    return prev[k];
}

bool canPartition(vector<int> &arr, int n) {
	int sum = 0;

	for (int i=0; i<n; i++) sum += arr[i];

	if (sum % 2) return false;

	int target = sum / 2;

	return subsetSumToK(n, target, arr);
}

```

## Analysis

- **Time Complexity**: `O(n * target)`
- **Space Complexity**: `O(target)`

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/partition-equal-subset-sum-_892980

## Tags

#dp #recursion #sum #equal #subsequence #subset #subset-sum 
# 16. Partition A Set Into Two Subsets With Minimum Absolute Sum Difference

## Description

- Use 14th question approach.

## Space Optimization

```cpp
int minSubsetSumDifference(vector<int>& arr, int n) {
	
	int totSum = 0;

	for (int i=0; i<n; i++) totSum += arr[i];

	int k = totSum / 2;

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

	int miniDiff = 1e9;

	for (int i=0; i<=k; i++) {
		if (prev[i] == true) {
			int absDiff = abs(i - (totSum - i));
			miniDiff = min(miniDiff, absDiff);
		}
	}

	return miniDiff;
}

```

## Analysis

- **Time Complexity**: `O(n * target)`
- **Space Complexity**: `O(target)`


---

## Resources

- **Problem Link**: https://www.naukri.com/code360/problems/partition-a-set-into-two-subsets-such-that-the-difference-of-subset-sums-is-minimum_842494

## Tags

#dp #recursion #subset-sum #sum #subset #subsequence #minimization 

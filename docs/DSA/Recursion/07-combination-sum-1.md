# 7. Combination Sum 1

## Description

- From a list of distinct numbers, find all unique combinations which sums to target. Same element can be taken more than once.

## Solution

```cpp
class Solution {
public:
    void recurse(int ind, int target, vector<int> &arr, vector<int> &ds, vector<vector<int>> &ans) {
        if (ind == arr.size()) {
            if (target == 0) ans.push_back(ds);
            return;
        }

        // take
        if (arr[ind] <= target) {
            ds.push_back(arr[ind]);
            recurse(ind, target - arr[ind], arr, ds, ans);
            ds.pop_back();
        }

        // not-take
        recurse(ind + 1, target, arr, ds, ans);
    }

    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> ans;
        vector<int> ds;

        recurse(0, target, candidates, ds, ans);

        return ans;
    }
};
```

## Analysis

- **Time Complexity**: `O(2^t * k)`
- **Space Complexity**: `O(k * x)`

## Resources

- **Problem Link**: https://leetcode.com/problems/combination-sum/

## Tags

#recursion #take-not-take #sum #combination-sum

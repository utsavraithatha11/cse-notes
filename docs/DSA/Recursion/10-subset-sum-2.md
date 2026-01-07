# 10. Subset Sum 2

## Description

- Return all possible subsets of an array. The array can contain duplicates.

## Solution

```cpp
class Solution {
public:
    void recurse(int ind, vector<int> &nums, vector<int> &ds, vector<vector<int>> &ans) {
        ans.push_back(ds);

        for (int i=ind; i<nums.size(); i++) {
            if (i > ind && nums[i] == nums[i-1]) continue;

            ds.push_back(nums[i]);
            recurse(i + 1, nums, ds, ans);
            ds.pop_back();
        }
    }

    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        vector<vector<int>> ans;
        vector<int> ds;

        sort(nums.begin(), nums.end());

        recurse(0, nums, ds, ans);

        return ans;
    }
};
```

## Analysis

- **Time Complexity**: `O(2^n * n)`
- **Space Complexity**: `O(2^n * k)`

## Resources

- **Problem Link**: https://leetcode.com/problems/subsets-ii
## Tags

#recursion #sum #subset-sum #subset

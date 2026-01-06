## Description

- Return all the permutation of an array with distinct elements.

## Solution 1 - Using boolean taken array

```cpp
class Solution {
public:
    void recurse(vector<int> &nums, vector<int> &ds, vector<bool> &taken, vector<vector<int>> &ans) {
        if (ds.size() == nums.size()) {
            ans.push_back(ds);
            return;
        }

        for (int i=0; i<nums.size(); i++) {
            if (!taken[i]) {
                taken[i] = true;
                ds.push_back(nums[i]);
                recurse(nums, ds, taken, ans);
                ds.pop_back();
                taken[i] = false;        
            }
        }
    }

    vector<vector<int>> permute(vector<int>& nums) {
        int n = nums.size();

        vector<vector<int>> ans;
        vector<int> ds;
        vector<bool> taken(n, 0);

        recurse(nums, ds, taken, ans);

        return ans;
    }
};
```

## Analysis

- **Time Complexity**: `O(n! * n)`
- **Space Complexity**: `O(n)`

## Solution 2 - Without taken array; using swapping

```cpp
class Solution {
public:
    void recurse(int ind, vector<int> &nums, vector<vector<int>> &ans) {
        if (ind == nums.size()) {
            ans.push_back(nums);
            return;
        }

        for (int i=ind; i<nums.size(); i++) {
            swap(nums[i], nums[ind]);
            recurse(ind + 1, nums, ans);
            swap(nums[i], nums[ind]);
        }
    }

    vector<vector<int>> permute(vector<int>& nums) {
        int n = nums.size();

        vector<vector<int>> ans;

        recurse(0, nums, ans);

        return ans;
    }
};
```

## Analysis

- **Time Complexity**: `O(n! * n)`
- **Space Complexity**: `O(n)`

## Notes

Approach 2:

![[Pasted image 20250319125454.png]]
## Resources

- **Problem Link**: https://leetcode.com/problems/permutations/

## Tags

#recursion #permutation 
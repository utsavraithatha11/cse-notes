## Description

- From a list of numbers, find all unique combinations which sums to target. Each number can be used only once in a combination.

## Solution

```cpp
class Solution {
    public:
        void recurse(int ind, int target, vector<int> &arr, vector<int> &ds, vector<vector<int>> &ans) {
            if (target == 0) {
                ans.push_back(ds);
                return;
            }
    
            for (int i=ind; i<arr.size(); i++) {
                if (i > ind && arr[i] == arr[i-1]) continue;
    
                if (arr[i] > target) break;
    
                ds.push_back(arr[i]);
                recurse(i + 1, target - arr[i], arr, ds, ans);
                ds.pop_back();
            }
        }
    
        vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
            sort(candidates.begin(), candidates.end());
            vector<int> ds;
            vector<vector<int>> ans;
    
            recurse(0, target, candidates, ds, ans);
    
            return ans;
        }
    };
```

## Analysis

- **Time Complexity**: `O(2^t * k)`
- **Space Complexity**: `O(k * x)`

## Notes

- ![[Pasted image 20250318202820.png]]

## Resources

- **Problem Link**: https://leetcode.com/problems/combination-sum-ii/

## Tags

#recursion #sum #combination-sum 
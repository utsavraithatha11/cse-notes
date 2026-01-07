# 9. Subset Sum 1

## Description

- Return the sums of all the subsets possible.

## Solution

```cpp
class Solution {
  public:
    void recurse(int ind, int &sum, vector<int> &arr, vector<int> &ans) {
        if (ind == arr.size()) {
            ans.push_back(sum);
            return;
        }
        
        // take
        sum += arr[ind];
        recurse(ind + 1, sum, arr, ans);
        sum -= arr[ind];
        
        // not-take
        recurse(ind + 1, sum, arr, ans);
    }
  
    vector<int> subsetSums(vector<int>& arr) {
        vector<int> ans;
        int sum = 0;
        
        recurse(0, sum, arr, ans);
        
        sort(ans.begin(), ans.end());
        
        return ans;
    }
};
```

## Analysis

- **Time Complexity**: `O(2^n)`
- **Space Complexity**: `O(2^n)`

## Resources

- **Problem Link**: https://www.geeksforgeeks.org/problems/subset-sums2234/1
## Tags

#recursion #subset #sum #subset-sum #take-not-take 
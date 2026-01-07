# 15. Palindrome Partitioning

## Description

- Return all possible partitions of strings which are all palindromes.

## Solution

```cpp
class Solution {
public:
    bool check_palindrome(int i, int j, string &s) {
        while (i < j) {
            if (s[i] != s[j])
                return false;
            i++;
            j--;
        }
        return true;
    }

    void recurse(int ind, string &s, vector<string> &ds, vector<vector<string>> &ans) {
        if (ind == s.size()) {
            ans.push_back(ds);
            return;
        }

        for (int i=ind; i<s.size(); i++) {
            if (check_palindrome(ind, i, s)) {
                ds.push_back(s.substr(ind, i - ind + 1));
                recurse(i + 1, s, ds, ans);
                ds.pop_back();
            }
        }
    } 

    vector<vector<string>> partition(string s) {
        vector<vector<string>> ans;
        vector<string> ds;

        recurse(0, s, ds, ans);

        return ans;      
    }
};
```

## Analysis

- **Time Complexity**: `O(2^n * n)`
- **Space Complexity**: `O(2^n * n)`

## Notes

![[Pasted image 20250319193125.png]]

## Resources

- **Problem Link**: https://leetcode.com/problems/palindrome-partitioning/

## Tags

#recursion #palindrome

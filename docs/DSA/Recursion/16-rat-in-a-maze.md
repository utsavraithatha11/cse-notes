# 16. Rat In A Maze

## Description

- Find all possible paths to go from (0, 0) to (n-1, n-1). 0 means water and 1 means land.

## Solution

```cpp
class Solution {
  public:
    vector<int> di = {1, 0, 0, -1};
    vector<int> dj = {0, -1, 1, 0};
  
    void recurse(int i, int j, vector<vector<int>> &mat, vector<vector<bool>> &vis, string &path, vector<string> &ans) {
    
        if (i == mat.size() - 1 && j == mat.size() - 1) {
            ans.push_back(path);
            return;
        }
        
        string dir = "DLRU";
        
        for (int ind=0; ind<4; ind++) {
            int x = i + di[ind];
            int y = j + dj[ind];
            
            if (x >= 0 && y >= 0 && x < mat.size() && y < mat.size() && !vis[x][y] && mat[x][y]) {
                vis[i][j] = true;
                path.push_back(dir[ind]);
                recurse(x, y, mat, vis, path, ans);
                path.pop_back();
                vis[i][j] = false;
            }
        }
    }
    
    vector<string> findPath(vector<vector<int>> &mat) {
        vector<string> ans;
        string path;
        int n = mat.size();
        vector<vector<bool>> vis(n, vector<bool>(n, 0));
        
        if (mat[0][0]) recurse(0, 0, mat, vis, path, ans);
        
        return ans;
    }
};
```

## Analysis

- **Time Complexity**: `O(4^(n*m))`
- **Space Complexity**: `O(n*m)`

## Notes

![[Pasted image 20250319195919.png]]

## Resources

- **Problem Link**: https://www.geeksforgeeks.org/problems/rat-in-a-maze-problem/1
## Tags

#recursion #land-water #grid
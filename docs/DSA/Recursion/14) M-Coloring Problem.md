## Solution

```cpp
class Solution {
  public:
    bool isValid(int node, int color, vector<vector<int>> &adj, vector<int> &col) {
        for (auto ngbr : adj[node]) {
            if (col[ngbr] == color)
                return false;
        }
        
        return true;
    }
  
    bool recurse(int node, int &v, int &m, vector<vector<int>> &adj, vector<int> &col) {
        if (node == v)
            return true;
            
        for (int i=1; i<=m; i++) {
            if (isValid(node, i, adj, col)) {
                col[node] = i;
                if (recurse(node + 1, v, m, adj, col)) return true;
                col[node] = 0;
            }
        }
        
        return false;
    }
    
    bool graphColoring(int v, vector<pair<int, int>>& edges, int m) {
        vector<vector<int>> adj(v);
        
        for (auto &edge : edges) {
            adj[edge.first].push_back(edge.second);
            adj[edge.second].push_back(edge.first);
        }
        
        vector<int> col(v, 0);
        
        return recurse(0, v, m, adj, col);
    }
};
```

## Analysis

- **Time Complexity**: `O(N^M)` N = no of nodes, M = colors
- **Space Complexity**: `O(N)`

## Resources

- **Problem Link**: https://www.geeksforgeeks.org/problems/m-coloring-problem-1587115620/1

## Tags

#recursion #m-coloring
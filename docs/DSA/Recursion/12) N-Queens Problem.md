## Description

- For n sized chessboard, place n queens such that:
	- Each row has exactly 1 queen
	- Each col has exactly 1 queen
	- Queens should not attach each other

## Solution 1

```cpp
class Solution {
public:

    bool isValid(int row, int col, int &n, vector<string> &board) {
        
        // check left
        for (int c=0; c<col; c++) {
            if (board[row][c] == 'Q') return false;
        }

        // check upper-diagonal
        int r = row - 1, c = col - 1;
        while (r >= 0 && c >= 0) {
            if (board[r][c] == 'Q') return false;
            r--;
            c--;
        }

        // check lower-diagonal
        r = row + 1, c = col - 1;
        while (r < n && c >= 0) {
            if (board[r][c] == 'Q') return false;
            r++;
            c--;
        }

        return true;
    }

    void recurse(int col, int &n, vector<string> &board, vector<vector<string>> &ans) {
        if (col == n) {
            ans.push_back(board);
            return;
        }

        for (int row=0; row<n; row++) {
            if (isValid(row, col, n, board)) {
                board[row][col] = 'Q';
                recurse(col + 1, n, board, ans);
                board[row][col] = '.';
            }
        }
    }

    vector<vector<string>> solveNQueens(int n) {
        string s(n, '.');
        vector<vector<string>> ans;
        vector<string> board(n, s);

        recurse(0, n, board, ans);

        return ans;
    }
};
```

## Analysis

- **Time Complexity**: `O(n^2 * n!)` due to pruning n^n is reduced to n!
- **Space Complexity**: `O(n^2 + n!)`

## Solution 2 - Optimizing isSafe Logic

```cpp
class Solution {
public:

    vector<int> leftRow, lowDiag, upDiag;

    void recurse(int col, int &n, vector<string> &board, vector<vector<string>> &ans) {
        if (col == n) {
            ans.push_back(board);
            return;
        }

        for (int row=0; row<n; row++) {
            if (!leftRow[row] && !upDiag[(n - 1) + (col - row)] && !lowDiag[row + col]) {
                board[row][col] = 'Q';
                
                leftRow[row] = true;
                lowDiag[row + col] = true;
                upDiag[(n - 1) + (col - row)] = true;
                
                recurse(col + 1, n, board, ans);
                
                board[row][col] = '.';
                
                leftRow[row] = false;
                lowDiag[row + col] = false;
                upDiag[(n - 1) + (col - row)] = false;
            }
        }
    }

    vector<vector<string>> solveNQueens(int n) {
        string s(n, '.');
        vector<vector<string>> ans;
        vector<string> board(n, s);

        leftRow.resize(n, 0);
        lowDiag.resize(2*n - 1, 0);
        upDiag.resize(2*n - 1, 0);

        recurse(0, n, board, ans);

        return ans;
    }
};
```

## Analysis

- **Time Complexity**: `O(n * n!)`
- **Space Complexity**: `O(n^2 + n!)`

## Notes

 ![[Pasted image 20250319132401.png]]

For optimizing isSafe Logic
![[Pasted image 20250319134959.png]]
## Resources

- **Problem Link**: https://leetcode.com/problems/n-queens/
## Tags

#recursion #n-queens
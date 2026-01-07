# 13. Sudoku Solver

## Solution

```cpp
class Solution {
public:
    bool isValid(char chr, int r, int c, vector<vector<char>>& board) {
        for (int i=0; i<9; i++) {
            // row
            if (chr == board[r][i]) return false;

            // col
            if (chr == board[i][c]) return false;

            // box
            if (chr == board[3 * (r/3) + i/3][3 * (c/3) + i%3]) return false;
        }

        return true;
    }

    bool recurse(vector<vector<char>>& board) {
        for (int r=0; r<board.size(); r++) {
            for (int c=0; c<board.size(); c++) {
                if (board[r][c] == '.') {
                    for (char chr = '1'; chr <= '9'; chr++) {
                        if (isValid(chr, r, c, board)) {
                            board[r][c] = chr;

                            if (recurse(board))
                                return true;
                            else
                                board[r][c] = '.';
                        }
                    }

                    return false;
                }
            }
        }

        return true;
    }

    void solveSudoku(vector<vector<char>>& board) {
        recurse(board);
    }
};
```

## Analysis

- **Time Complexity**: `O(9^81)` in worst case but much lower in practical scenarios due to pruning and constraints.
- **Space Complexity**: `O(81) = O(1)`

## Notes

![[Pasted image 20250319143838.png]]

## Resources

- **Problem Link**: https://leetcode.com/problems/sudoku-solver/
## Tags

#recursion #sudoku 

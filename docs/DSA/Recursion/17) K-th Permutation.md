## Solution

- Do recursion and find the kth permutation. 
- But it would be a brute force.
- Here is the optimal solution.

```cpp
class Solution {
public:
    string getPermutation(int n, int k) {
        vector<int> v(n);
        string ans = "";

        for (int i=0; i<n; i++) v[i] = i + 1;

        int fact = 1;
        for (int i=1; i<n; i++) fact *= i;
        k--;

        while (n != 1) {
            int ind = k / fact;
            ans += v[ind] + '0';
            v.erase(v.begin() + ind);
            k = k % fact;
            n--;
            fact /= n;
        }

        ans += v[0] + '0';

        return ans;
    }
};
```

## Analysis

- **Time Complexity**: `O(n*n) = O(n^2)`
	- 1st n for all the numbers in a permutation
	- 2nd n for erasing that number from the left array
- **Space Complexity**: `O(n)`

## Notes

![[Pasted image 20250319224709.png]]

## Resources

- **Problem Link**: https://leetcode.com/problems/permutation-sequence/
## Tags

#recursion 
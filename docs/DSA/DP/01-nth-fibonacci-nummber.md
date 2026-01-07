# 1. Nth Fibonacci Nummber

## Solutions
## 1) Memorization

```cpp
#include <bits/stdc++.h>
using namespace std;

#define ll long long
#define pb push_back

int f(int n, vector<int> &dp) {
    if (n <= 1) return 1;

    if (dp[n] != -1) return dp[n];

    return dp[n] = f(n-1, dp) + f(n-2, dp);
}

void solve() {
    int n;
    cin >> n;
    
    vector<int> dp(n + 1, -1);
    cout << f(n, dp);
}

int main() {
    solve();

    return 0;
}
```

## Analysis

- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(n) + O(n)` rec stack space + dp array


---

## 2) Tabulation

```cpp
#include <bits/stdc++.h>
using namespace std;

#define ll long long
#define pb push_back

void solve() {
    int n;
    cin >> n;
    
    vector<int> dp(n + 1, -1);
    dp[0] = 1;
    dp[1] = 1;

    for (int i=2; i<=n; i++) {
        dp[i] = dp[i-1] + dp[i-2];
    }

    cout << dp[n];
}

int main() {
    solve();

    return 0;
}
```

## Analysis

- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(n)`


---

## 3) Space Optimization

```cpp
#include <bits/stdc++.h>
using namespace std;

#define ll long long
#define pb push_back

void solve() {
    int n;
    cin >> n;
    
    int prev2 = 0, prev = 1;
    int curr;

    if (n <= 1) {
        cout << n;
        return;
    }

    for (int i=2; i<=n; i++) {
        curr = prev + prev2;
        prev2 = prev;
        prev = curr;
    }

    cout << curr;
}

int main() {
    solve();

    return 0;
}
```

## Analysis

- **Time Complexity**: `O(n)`
- **Space Complexity**: `O(1)`

## Tags

#recursion #dp #fibonacci
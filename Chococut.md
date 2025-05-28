## Chococut

## Language: C++

We’re given a chocolate bar of size N × M (grid). Alice can cut it once (or not at all), and Bob wants at least K squares. Alice wants to maximize what she keeps.

### Processing the Problem Statement

The total number of squares is `N * M`.  
Since Alice can only cut once, the bar can be divided into two rectangles: either by horizontal cut or vertical cut.  
Bob should get *at least* K squares, so we need to try all possible cuts, and:
  - See if one of the pieces satisfies Bob's requirement.
  - If yes, take the size of the other piece as Alice's share.
  - Track the **maximum** Alice can keep across all valid cuts.

### Edge Cases

- K = 0: Bob needs nothing. Alice keeps the full chocolate.
- K > N * M: Not possible by problem constraint; doesn't need handling.

```cpp
if (k == 0) {
            cout << n * m << endl;
            continue;
        }
```

### Final Approach

1. Iterate through **all horizontal cuts** 
   - One piece = `i * M`, other = `(N - i) * M`.
```cpp
 for (int i = 1; i < n; i++) {
            int bob = i * m;
            if (bob >= k) {
                int alice = (n - i) * m;
                maxA = max(maxA, alice);
            }
            bob = (n - i) * m;
            if (bob >= k) {
                int alice = i * m;
                maxA = max(maxA, alice);
            }
        }
```
2. Similarly, **all vertical cuts**  
   - One piece = `N * j`, other = `N * (M - j)`.
3. For each division:
   - Check if either part is >= K (Happy Bob).
   - Track the max size of the remaining part (Alice's part).

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int t; cin >> t; 
    while (t--) {
        int n, m, k;
        cin >> n >> m >> k;

        int maxA = 0;

        if (k == 0) {
            cout << n * m << endl;
            continue;
        }

        for (int i = 1; i < n; i++) {
            int bob = i * m;
            if (bob >= k) {
                int alice = (n - i) * m;
                maxA = max(maxA, alice);
            }
            bob = (n - i) * m;
            if (bob >= k) {
                int alice = i * m;
                maxA = max(maxA, alice);
            }
        }

        for (int j = 1; j < m; j++) {
            int bob = n * j;
            if (bob >= k) {
                int alice = n * (m - j);
                maxA = max(maxA, alice);
            }
            bob = n * (m - j);
            if (bob >= k) {
                int alice = n * j;
                maxA = max(maxA, alice);
            }
        }

        cout << maxA << endl; // Output max Alice can keep
    }

    return 0;
}


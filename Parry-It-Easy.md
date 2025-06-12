# Parry It (Easy)
## Language: C++; Time Complexity: O(N); Concept: Greedy,  Suffix Maximum

- We want to parry as many times as possible without losing the game. Since X >= A[i], losing the game is impossible.  
- Since parrying costs one energy, we need to check if we can afford to lose that one energy point.  
- If we want to parry at ith index we must check if X >= B[i] and if X-1 >= for all A[j] where j>i.  
(if X<A[j] dodging becomes impossible, chef loses the game.)

My initial approach to check for the max value of A after ith index was a bubble loop.
```cpp

        for (int i = 0; i < n; i++) {
            int m = 0;
            for (int j = i + 1; j < n; j++) {
                m = max(m, a[j]);
            }
            maxFuture[i] = m;
        }

```
but the nested loop brings T.C. to O(N^2), obvious TLE.

So, I tried suffix maximum.  
```cpp

maxFuture[N] = 0;
for (int i = N - 1; i >= 0; i--)
maxFuture[i] = max(maxFuture[i + 1], A[i]);

```
I defined a vector maxFuture to size N+1 to store a dummy value of 0 on the Nth index so that for i=N the operation does not go out of bounds.

### Final Code:
``` cpp

#include <bits/stdc++.h>
using namespace std;

int main() {
    int t; cin >> t;

    while (t--) {
        int n,x; cin >> n >> x;

        vector<int> a(n), b(n), maxFuture(n + 1);
        for (int i = 0; i < n; i++) cin >> a[i];
        for (int i = 0; i < n; i++) cin >> b[i];

        maxFuture[n] = 0;
        for (int i = n - 1; i >= 0; i--)
        maxFuture[i] = max(maxFuture[i + 1], a[i]);

        int p = 0;

        for (int i = 0; i < n; i++) {
            if (x >= b[i] && x- 1 >= maxFuture[i + 1]) {
                x--;
                p++;
            }
        }

        cout << p << endl;
    }

}

```

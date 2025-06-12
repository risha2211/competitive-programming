# False Alarm
## Language: GNU G++17 7.3.0 (C++); Time Complexity: O(N); Concept: Greedy

- Yousef first passes through as many open doors as he can.
- When he encounters the first closed door, he deploys the button.
- The doors open for x seconds, aka he passes through exactly x doors irrespective of their open/close status.
- After x seconds, initially closed doors would close again.
- Now if Yousef comes across another closed door (1), he fails. Output: NO.
- If all doors are now open (0), he wins. Output: YES.

TL;DR: Yousef can press this button at most once. It will open all closed doors for exactly x seconds. He must finish passing through any closed doors within those x seconds (x consecutive doors).


```cpp
#include <bits/stdc++.h>
using namespace std;
 
int main() {
    int t; cin >> t;
    while (t--) {
        int n, x; cin >> n >> x;
 
        vector<int> a(n);
        for (int i = 0; i < n; i++) cin >> a[i];
 
        int first_closed;
        for (int i = 0; i < n; i++) {
            if (a[i] == 1) {
                first_closed = i;
                break;
            }
        }
 
        bool ok = true;
        for (int i = first_closed + x; i < n; i++) {
            if (a[i] == 1) {
                ok = false;
                break;
            }
        }
 
        cout << (ok ? "YES\n" : "NO\n");
    }
}
```

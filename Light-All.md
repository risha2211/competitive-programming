# Light All
## Language: C++; Time Complexity: O(N); Concept: Greedy

There are N lights. Our goal is to determine whether or not all lights can be lit. 

### Thought Process:  
- We have to iterate through a binary string.  
- If the ith index is 1 (aka the lamp is lit), move onto i+1.  
- If the ith index is 0, check whether the lamp can recieve light from either side.
- To be able to light up, the adjacent index to the 0th index should be 1 and should not be facing in the opp. direction (supplying light to a different lamp).
- We must first check whether a dim light can accept light from a lamp on its left, then from right. (right first may lead to missed lamps. E.g.: 1010)

### Code Implementation:
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int t; cin >> t;
    while (t--) {
        int n; string s;
        cin >> n >> s;

        vector<bool> used(n, false);  // To keep a track of which lit lamps are used already
        bool poss = true;

        for (int i = 0; i < n; i++) {
            if (s[i] == '1')
            continue; // next iteration

            bool lit = false;

            // borrow left
            if (i > 0 && s[i - 1] == '1' && !used[i - 1]) { // cannot borrow from left on 0th index
                used[i - 1] = true;
                lit = true;
            }
            // else borrow right
            else if (i + 1 < n && s[i + 1] == '1' && !used[i + 1]) { // cannot borrow from left on (n-1)th index
                used[i + 1] = true;
                lit = true;
            }

            if (!lit) {
                poss = false;
                break;
            }
        }

        cout << (poss ? "Yes" : "No") << endl;
    }
}

```


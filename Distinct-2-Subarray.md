# Distinct 2 Subarray

## Language: C++; Time Complexity: O(N^2); Concept: Hash Map, Brute Force 


``` cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	int t; cin >> ;t
    while (t--) {
        int n; cin >> n;
        vector<int> a(n);
        for (int i = 0; i < n; i++)
        cin >> a[i];

        int ans = n + 1;
        for (int i = 0; i < n; i++) {
            unordered_map<int, int> f;
            for (int j = i; j < n; j++) {
                f[a[j]]++;
                if (f.size() > 2) 
                break;
                if (f.size() == 2)
                    ans = min(ans, j - i + 1);
            }
        }
        cout << (ans == n + 1 ? -1 : ans) << endl;
    }
}
```
### Breakdown:
```cpp
int ans = n + 1;
```
- Stores the minimum length of any good subarray found.
- Initialized to a value larger than any valid subarray length.

```cpp
for (int i = 0; i < n; i++) {
    unordered_map<int, int> f;
    for (int j = i; j < n; j++) {
        f[a[j]]++;
        if (f.size() > 2)
        break;
        if (f.size() == 2)
            ans = min(ans, j - i + 1);
    }
}
```
Outer loop starts the subarray from every index i.   
Inner loop extends the subarray from i to j.  
unordered_map<int, int> f acts like a dictionary.

Key -> element value (e.g., 1, 2, 3)  
Value -> count of how many times that element has occurred in the current subarray [i...j]

```cpp
f[a[j]]++
```
Adds current element to the frequency map or increments its count.

if (f.size() > 2) break;   
As soon as more than 2 distinct elements are seen, the subarray can't be good.

if (f.size() == 2)  
If exactly 2 distinct elements are in the map, it’s a good subarray.

Update ans with the length j - i + 1 if it's smaller than previous best.





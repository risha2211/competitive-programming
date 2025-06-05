# Sqaure Year

## Language: C++; Time Complexity: O(N)

We are given a year (as a string S) and asked to determine whether it can be expressed in the form `(a+b)^2` where a and b are any non-negative integers.  
This simplifies to checking whether the number n (converted from S) is a perfect square.
- Convert the string to an integer using stoi(S).
- If n is a perfect square, any valid pair (a, b) such that a + b = sqrt(n) will work. The simplest choice is a = 0, b = sqrt(n).
- Otherwise, return -1.

```cpp
#include <bits/stdc++.h>
using namespace std;
 
int main() {
    int t; cin >> t;
    while (t--) {
        string s; cin >> s;
        int n = stoi(s);
        int r = (int)(sqrt(n));
        if (r * r == n)
        cout << 0 << " " << r << endl; // Space between a and b to match sample output format.
        else
        cout << -1 << endl;
    }
}
```

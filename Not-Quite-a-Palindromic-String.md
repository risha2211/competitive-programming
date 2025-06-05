# Not Quite a Palindromic String
## Language : GNU G++17 7.3.0 (C++); Time Complexity: O(N); Concept: Brute Force

Given a binary string `s` of even length `n`, the goal is to rearrange characters such that there are exactly `k` good pairs.  
A pair (i, n - i + 1) is good if s[i] == s[n - i + 1], making a total of n/2 pairs possible.

### Code Logic

Let:
- `c0` be the number of 0s in the string.
- `c1` be the number of 1s in the string.  

The total number of good pairs possible is n / 2.  

- `k` = total number of good pairs.   
- `c = pairs - k` will be the number of bad pairs. 
- Each good pair consists of two matching characters (0 0 or 1 1).  

For a fixed value `a` (number of good pairs made from 0), let `b = k - a` (remaining good pairs are from 1).

- 2 * a + c zeroes are needed (2 per good pair, 1 per bad pair).
- 2 * b + c ones are needed.

If the available c0 and c1 are sufficient to meet this requirement for any (a, b) pair such that a + b = k, then a rearrangement is possible.

```cpp

#include <bits/stdc++.h>
using namespace std;
 
bool pair(int n, int k, const string& s) {    // s is called by reference as a constant to ensure it is not modified inside the function.
    int c0 = 0, c1 = 0;
    for (char c : s) {          // for-each loop to iterate over each character in the string
        if (c == '0') c0++;
        else c1++;
    }
 
    int pairs = n / 2;
    int c = pairs - k; 
    
    for (int a = 0; a <= k; a++) {
        int b = k - a;
        if (2*a + c <= c0 && 2*b + c <= c1) {
            return true;
        }
    }
    return false;
/* As soon as a valid (a, b) pair is found, the function terminates immediately by returning true,  
skipping the rest of the loop. If no such pair is found, function returns false. */
}
 
int main() {

    int t; cin >> t;
    while (t--) {
        int n, k; string s;
        cin >> n >> k >> s;
        if (pair(n, k, s))
            cout << "YES" << endl;
        else
            cout << "NO" << endl;
    }
}

```


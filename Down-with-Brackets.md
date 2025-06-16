# Down with Brackets
## Language : GNU G++17 7.3.0 (C++); Time Complexity: O(N); Concept: Balance Factor

A balanced bracket sequence is one that has a opening bracket before a closing bracket. 
Balanced bracket sequence examples: `(())`, `()()`, `((()()))`  
Unbalanced bracket sequence examples: `(()` `(()))(`

We need to check whether we can convert a given balanced sequence of brackets into unbalanced by removing any one opening bracket and any one closing bracket. 

For this I applied the concept of balance factor: 
- Define a variable f for balance factor and initialise it to 0.
- Iterate through the string of brackets from right to left.
- Add 1 for every '('
- Subtract 1 for every ')'
- If the value of f becomes 0 before the last closing bracket, it can be converted into an unbalanced seq, else no

E.g.:
for ()(), variation of f throughout the string- [1,0,1,0]. Removing the first and last brackets makes it unbalanced. ✅
for (()), variation of f- [1,2,1,0]. Impossible to make it unbalanced. ❌

```cpp#include <iostream>
#include <bits/stdc++.h>
using namespace std;
 
int main() {
    int t; cin >> t;

    while (t--) {
        string s; cin>>s;
 
        int f = 0;
        bool poss = false;
 
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '(')
            f++;
            else
            f--;
 
            if (f == 0 && i != s.size() - 1) {
                poss = true;
                break;
            }
        }
 
        cout << (poss ? "YES" : "NO") << endl;
    }
}

```



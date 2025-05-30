# Red and Blue Gems

## Language: C++

To get the maximum coins:
Calculate total value if you take all red gems: R × P  
Calculate total value if you take all blue gems: B × Q  
Return the maximum of the two.

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	// your code goes here
    int r,b,p,q; cin>>r>>b>>p>>q;
    if (r*p > b*q)
    cout << r*p <<endl;
    else
    cout << b*q <<endl;
    return 0;
}
```

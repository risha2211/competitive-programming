# Incremental Game

## Language: C++; Time Complexity: O(1); Concept: Greedy

Alice draws the first pile where the number of stones is less than or equal to K. Then Bob. Then Alice, and so on...  
It is in both of their best interest to draw as many stones as possible in one go.  

There are 3 possible cases:

1. k >= x and k >= y

In this scenario, Alice will choose the bigger pile and remove all the stones from it. It will be impossible for Bob to remove **more**
stones than Alice. Hence, Alice wins.

2. k < x and k < y

In this scenario, Alice cannot clear the whole pile.  
E.g.:
- `x=5, y=6, k=2`;
Alice chooses the y pile and removes 2 stones from it, Bob will clear out the entire x pile.

- `x=5, y=10, k=2`
Alice chooses the y pile and removes 2 stones from it, Bob will clear out the remaining y pile.

In short, Bob will chose max(x,y-k), which will always be greater than k. Hence, Bob wins.

3. x <= k < y (or y <= k < x)

In this scenario, Alice chooses the y pile (choosing x would mean Bob clearing out y pile and Alice losing) and removes k stones from it.  
Bob can now either clear x pile or clear out the remaaining stones in y (y-k). Since x=<k, Bob **cannot** remove from the x pile  
and can only draw y-k stones.  If (y-k) > k, Bob wins. Otherwise, Alice wins. 
E.g.:
- `x=2, y=7, k=3`
Alice removes 3 stones from y resulting in y having 4 stones. Bob then removes the 4 stones and wins. 
- `x=3, y=5, k=3`
Alice removes 3 stones from y resulting in y having 2 stones. Bob loses. 

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int t; cin >> t;
    while (t--) {
        int x, y, k; cin >> x >> y >> k;

        if (x > y) 
        swap(x, y);

        if (k >= y)
        cout << "Alice" << endl;
        else if (k < x)
        cout << "Bob" << endl;
        else{
            if (y - k > k)
            cout << "Bob" << endl;
            else
            cout << "Alice" << endl;
            }
    }
}
```
Always make y>=x to simplify the code and avoid multiple cases !



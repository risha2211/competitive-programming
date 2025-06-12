# Nutrition Cost
## Language: C++; Time Complexity: O(N)

We are given a natural number X and by performing certain operations our goal is to reduce it to the smallest possible number. 
`if X>3, X-= 3`  - OP1
`if X is even, X/=2` - OP2

**Thought Process:**

- if X is less than 3:  
        X=1, X unchanged  
        X=2, X= 2/2= 1  
        X=3, X unchanged
  
- if X is odd and greater than 3, subtracting 3 is the only and the correct choice.
- if X is even and greater than 3 we ought to choose the operation that gives the smallest answer.
        A series of X/2 operations will always result in Xmin being 1.
        X/=2 is also a more rapidly decreasing function compared to X-=3.
        However for X<6 X-=3 < X/=2 (i.e. for X=4). So, it is more efficient to perform X-=3 (1 step) on X= 4 than X/2 twice.

On considering every case, this was my code:

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int t; cin >> t;
    while (t--) {
        int x; cin >> x;

        while (1) {
            if (x % 2 == 0 && x!= 4) x /= 2;
            else if (x == 4) x -= 3;
            else if (x > 3) x -= 3;   
            else break;
        }

        cout << x << endl;
    }
    return 0;
}

```

However, when I revisited the question post contest I realised the question never asked to minimise the number of steps nor does the route taken affect the final output.  
The optimal approach would have been to just divide any even number by 2 as it will always result in Xmin (1) and to subtract 3 from any odd number greater than 3, as follows:

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int t; cin >> t;
    while (t--) {
        int x; cin >> x;

        while (1) {
            if (x % 2 == 0) x /= 2;
            else if (x > 3) x -= 3;
            else break;
        }

        cout << x << endl;
    }
    return 0;
}

```

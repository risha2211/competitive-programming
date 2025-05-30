# Subset Sum 3

## Language: C++

**Given a set, we need to check if there exists any non-empty subset whose sum is divisible by 3.**

We don’t want to try every subsequence. That would be very slow and inefficient.  

If the sum of some numbers is divisible by 3, then we’re done.  

`0 % 3 == 0` -> Divisible by 3  
`0 % 3 == 1` -> Remainder = 1  
`0 % 3 == 2` -> Remainder = 2  

We count how many numbers fall into each of these categories and check if it’s possible to form a subsequence whose sum is divisible by 3 using these remainders.  

- Case 1: If any number is divisible by 3, we pick that number.
- Case 2: If there’s at least one number that's 1 mod 3 and at least one that's 2 mod 3, we pick them. (1+2=3)
- Case 3: If there are at least three numbers that are 1 mod 3, we pick them. (1+1+1=3)
- Case 4: Similarly, if there are at least three numbers that are 2 mod 3, we pick them. (2+2+2=3)

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int T; cin >> T;

    while (T--) {
        int N;
        cin >> N;
        vector<int> A(N);
        int mod0 = 0, mod1 = 0, mod2 = 0;

        for (int i = 0; i < N; ++i) {
            cin >> A[i];
            int rem = A[i] % 3;
            if (rem == 0) mod0++;
            else if (rem == 1) mod1++;
            else mod2++;
        }

        if (mod0 >= 1 || (mod1 >= 1 && mod2 >= 1) || mod1 >= 3 || mod2 >= 3)
            cout << "Yes" << endl;
        else
            cout << "No" << endl;
    }

    return 0;
}
```

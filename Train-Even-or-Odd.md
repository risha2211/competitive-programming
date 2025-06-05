# Train Even or Odd

## Language: C++; Time Complexity: O(N)

Create two sums:  
odd_sum = total hours on odd days (indices 0, 2, 4, ...)  
even_sum = total hours on even days (indices 1, 3, 5, ...)  
Return the maximum of the two.  

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int T;
    cin >> T;
    
    while (T--) {
        int N;
        cin >> N;
        vector<int> A(N);
        for (int i = 0; i < N; ++i) {
            cin >> A[i];
        }

        int odd_sum = 0, even_sum = 0;
        for (int i = 0; i < N; ++i) {
            if (i % 2 == 0) // since i=0 is 1st index aka odd day
                odd_sum += A[i];
            else
                even_sum += A[i];
        }

        cout << max(odd_sum, even_sum) << endl;
    }

    return 0;
}

```

# Create Binary String

## Language: C++; Time Complexity: O(N); Concept: Greedy

We're given a binary string of length `N`, where cost of (non-contiguous):  
`0` = A  
`1` = B  
`01` = C
`10` = D

We have to rearrange the string to get the maximum coins.  
In a given string number of zeroes and ones will be constant.  
Let no. of 0s = i; no. of 1s = N-i;  
Therefore, i*A + (N-i)*B = constant   

So, we must maximise 01/10.    
If C > D or coins per 01 pair > coins per 10 pair, it will be in our best interest to turn all 10 pairs into 01.  
Similarly, if D > C, we turn all 01 pairs into 10. 

E.g.: if c>d for 0100110  
010110 -> 010101 -> 001101 -> 001011 -> 000111 ✅  
E.g.: if d>c for 110101  
110101 -> 111001 -> 111010 -> 111100 ✅  

We observe that for any c>d, all the 0s are lined up together in the beginning followed by all the 1s.    
Similarly, for ant d>c, all the 1s are lined up together in the beginning followed by all the 0s.  
Also note that every 0 pairs up with every 1 in every case.  
So, total pairs = total zeroes * total ones = i * (N - i)  

We create both pairs, 11..00 and 00..11 and finally output the highest value.  

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int t; cin >> t;
    while (t--) {
        int n, a, b, c, d; cin >> n >> a >> b >> c >> d;

        long long ans = 0;
        for (long long int i = 0; i <= n; i++) {
            ans = max(ans, (i*a + (n-i)*b + i*(n-i)*c));
            ans = max(ans, (i*a + (n-i)*b + i*(n-i)*d));
        }

        cout << ans << endl;;
    }

    return 0;
}
```






# It's Time To Duel

## Language: GNU G++17 7.3.0 (C++)

We have n players arranged in a line and they duel consecutively: player 1 vs player 2, player 2 vs player 3, ..., player (n-1) vs player n. Each duel produces exactly one winner and one loser.

After the duels, each player reports if they won at least one duel (report = 1) or none (report = 0).

Goal: check if there must be at least one liar among the players based on these reports.

- Since every duel produces exactly one winner and one loser, among n-1 duels, there cannot be more than n−1 wins in total. Therefore, if the total number of 1s is greater than n-1, someone is lying.

- If two consecutive players both say 0, that means neither won any duel. But these two players fought each other, so one must have won -impossible for both to say 0. Therefore, if there exist two consecutive zeros, someone is lying.

### How I Approached the Problem

First, I tried the simplest logic — check for any two adjacent zeros. Because the duel between them guarantees one winner, so both can’t have zero wins.  

Then I considered the sum of reports — it must be n-1, because there are exactly n-1 duels, and each duel produces exactly one winner.  

Combining both checks gives the final output:

- If either condition fails, print YES (there is a liar).
- Else, print NO (reports are consistent).

```cpp
#include <bits/stdc++.h>
using namespace std;
 
int main() {
 
    int t; cin >> t;
    while (t--) {
        int n; cin >> n;
        vector<int> a(n);
        for (int i = 0; i < n; i++) cin >> a[i];
 
        int liar = 0;
 
        for (int i = 0; i < n - 1; i++) {
            if (a[i] == 0 && a[i + 1] == 0) {
                liar = 1;
                break;
            }
        }
 
        int sum_a = 0;
        for (int i = 0; i < n; i++) {
            sum_a += a[i];
        }
 
        if (sum_a > n - 1) {
            liar = 1;
        }
 
        cout << (liar==1 ? "YES\n" : "NO\n");
    }
 
    return 0;
}
```

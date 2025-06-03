There are 3 energy crystals, numbered 1, 2, and 3.

Initially, all crystals have 0 energy.

Our goal is to charge each crystal to energy level 'x'.

Only one action can be performed at a time:

In one action, the energy level of any one crystal can be increased by any positive amount.

**Constraint (the tricky part):**

After every action, the following condition must hold:

For every pair of crystals i and j, it must be true that:

```cp
ai >= floor(aj/2)
```
where `ai` and `aj` are the current energy levels of the crystals.

This means:
No crystal can be significantly smaller than another.  
For example, if one crystal has energy 13, then every other crystal must be at least floor(13/2) = 6.  
This condition must be satisfied after **every** action.

Example: x=4.  
Start:  
A = 0, B = 0, C = 0

Now consider this (invalid) move:  
A = 4, B = 0, C = 0 ❌ Invalid  
Because B = 0, and floor(4/2)=2, so B < 2

Better approach:

A = 1  
B = 1  
C = 1

Then:  
A = 2  
B = 2  
C = 2 

And so on...

**Intuition:**  
The challenge is to reach the target value x using as few actions as possible while maintaining this balance.

code:
```cpp
#include <iostream>
using namespace std;

int main() {
    int t;
    cin >> t;
    while (t--) {
        long long x;
        cin >> x;

        int k = 0;
        long long value = 1;
        while (value <= x) {  // count until value > x
            value *= 2;
            k++;
        }
        k--;  // subtract 1 because we overshoot once

        int min_actions = 2 * k + 3;
        cout << min_actions << "\n";
    }
    return 0;
}
```
**Breakdown:**
```cpp
int k = 0;
long long value = 1;
while (value <= x) {  // count until value > x
    value *= 2;
    k++;
}
k--;  // subtract 1 because we overshoot once
```
This loop counts how many times you can double the number 1 before it becomes greater than 𝑥


value starts at 1.

On each iteration, it doubles value and increments k.

The loop stops when value becomes greater than 
𝑥
x.

Because the loop counts one extra step (when value just exceeded 
𝑥
x), we subtract 1 from k.



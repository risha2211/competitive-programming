# Energy Crystals

## Language: C++ (G++17 7.3.0)

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
        while (value <= x) { 
            value *= 2;
            k++;
        }
        k--;  

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
This loop counts how many times you can double the number 1 before it becomes greater than x.  
- value starts at 1.
- On each iteration, it doubles value and increments k.
- The loop stops when value becomes greater than x.  
- Because the loop counts one extra step (when value just exceeded x), we subtract 1 from k.

where k represents the largest exponent such that:  
2^k <= x  
so, k <= log₂x  

x may not be exactly a power of two.  
For example, if x= 20  
log₂20 ~ 4.32  
Because the crystals’ energy levels grow in doubling steps, the highest full doubling step you can take without exceeding x is at   
2^4 = 16

Therefore, k = floor(log₂x)

Why subtract 1 from k after the loop?

Say, x = 20:

- Iteration 1: `value = 1 * 2 = 2`, k = 1
- Iteration 2: `value = 2 * 2 = 4`, k = 2
- Iteration 3: `value = 4 * 2 = 8`, k = 3
- Iteration 4: `value = 8 * 2 = 16`, k = 4
- Iteration 5: `value = 16 * 2 = 32`, k = 5  
Now `value = 32` which is **greater than** x = 20 , so the loop stops.

However, on the 5th iteration, the value exceeded x, but k was incremented anyway.

So when the loop ends:  
k is 5, but the largest doubling step that did not exceed x is actually 2^4 = 16.  
To correct this, we subtract 1 from k.  

which matches floor(log₂20) = 4.  

### Intuition behind the formula:

- To reach energy level x, we need to double the energy levels multiple times because the crystals must stay balanced according to the constraint.
- Since the largest power of 2 less than or equal to x is 2^k, we need k doubling steps to reach near x.
- The +3 gets all the energy states from zero up to a base energy of 1.


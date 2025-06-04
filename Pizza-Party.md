# Pizza Party
## Language: C++

1. total_slices = (A + 1) * 4 + B * 3
2. pizzas = ceil(total_slices / 8.0)

```cpp
#include <iostream>
using namespace std;

int main() {
    int A, B;
    cin >> A >> B;

    int total_slices = (A + 1) * 4 + B * 3;
    int pizzas = ceil(float(total_slices)/ 8);

    cout << pizzas << endl;
    return 0;
}
```
- float(total_slices) converts the integer to float.
- Division / 8 gives you the exact number of pizzas needed (in decimal).
- ceil(...) rounds it up to the next whole number.

# Exercise and Rest [🔗](https://www.codechef.com/problems/EXREST?tab=statement)

## Language: C++, Time Complexity: O(1)

2 days exercise + 1 day rest = 3-day cycle

So if today is the N-th rest day, that means N 3 day cycles have passed.

Total days = 3 * N

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	// your code goes here
	int n; cin>>n;
	cout << 3*n<< endl;
	return 0;
}
```

# Fashionable Array

## Language: GNU G++17 7.3.0 (C++); Time Complexity: O(N^2)

### Problem Statement

We are given an array of size N and need to make it *fashionable* if it already isn't.  
For this the sum of the largest and smallest element needs to be even. We need to calculate the minimum number of steps aka the minimum elements we must delete from the array to make it fashionable.

---
### Logic
- If unmodified array is fashionable, operations=output=0. 
- Sort the array
- Create 2 loops, one that deletes elements from the right and one that deletes elements from the left. Keep track of no. of operations in both the loops and at last take the minimum of both.
- For this, we make a duplicate of the input array.
---

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	// your code goes here
	int t; cin>>t;
	while(t--){
	    int n; cin>>n;
	    vector <int> a(n), d(n);
	    for (int i=0; i<n; i++) cin>>a[i];
	    sort(a.begin(), a.end());
	    for (int i=0; i<n; i++) d[i]=a[i];
	    int lop=0, rop=0;
	    if ((a[0]+a[n-1])%2==0)
	    cout << 0 << endl;
	    else{
	        
	    while (a.size()>=0)
	    {
	        lop++;
	        a.erase(a.begin() + 0);
	        if (a.size()==1)
	        { if (a[0]%2==0) break;
	          else {lop++; break;}
	            }
	        else if ((a[0]+a[a.size()-1])%2==0) break;
	    }
	    
	    while (d.size()>=0)
	    {
	        rop++;
	        d.erase(d.begin() + d.size()-1);
	        if (d.size()==1)
	        { if (d[0]%2==0) break;
	           else {rop++; break;} }
	        else if ((d[0]+d[d.size()-1])%2==0) break;
	    }
	    
	    cout << min(lop,rop) << endl;
	    }
	    
	}

}

```
```cpp
if (a.size()==1)
	        { if (a[0]%2==0) break;
	          else {lop++; break;}
	            }
```
if the array consists only of a single number we check whether its even, if not, deleting it (op+=1) will make the array fashionable.





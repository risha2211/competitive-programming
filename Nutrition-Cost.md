# Nutrition Cost
## Language: C++; Time Complexity: O(NlogN); Concept: Greedy

Given `N` food items, each providing an essential vitamin `Ai` and costing `Bi`, the goal is to maximize the value:  
**CX-Y**
where:

- C is a constant
- X is the number of distinct vitamins
- Y is the total cost of the selected food items.

We are allowed to purchase no food items, wherein the output is zero.

### Approach

- For each distinct vitamin, it is optimal to purchase the food item offering that vitamin at the minimum cost. Minimising Y maximises CX-Y.

- Use a map to store the minimum cost for each vitamin. For each food item, if the vitamin is already present in the map, update its cost only if the current item’s cost is lower. Each insertion into a map is log N.

- Store the minimum costs of all distinct vitamins into a vector and sort it in ascending order. We then evaluate all possible subsets of vitamins, starting with the cheapest.

- Iterate through the sorted costs, keeping track of the maximum value obtained. This is the number of vitamins to be purchased.

- If no subset gives a positive value, output 0.

---

```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int t; cin>>t;
    while(t--)
    {
        int n,c; cin>>n>>c;
        vector <int> a(n), b(n);
        for (int i=0; i<n; i++) cin >> a[i];
        for (int i=0; i<n; i++) cin >> b[i];
        map <int,int> mp;
        for (int i=0; i<n; i++)
        {
        int v=a[i], cost=b[i];
        if (mp.count(v)) mp[v] = min(mp[v], cost);
        else mp[v] = cost;
        }
        vector<int> costs;
        for (auto it : mp) // auto assigns the type to the variables automatically. 
        {
        int vitamin = it.first;
        int cost = it.second;
        costs.push_back(cost);
        }
        sort(costs.begin(), costs.end());
        int sum = 0, ans = 0;
        for (int i = 0; i < costs.size(); i++) 
        {
        sum += costs[i];
        ans = max(ans, c*(i+1)-sum);
        }
        cout << ans << endl;
    }
}
```

### Breakdown of `vector<int> costs`

Let's say this is map mp with all the distinct vitamins and their minimum costs:
```cpp
mp = {
    2: 3,   //key:value pair
    4: 7,   
    7: 5
}
```
Now we just want to collect the values (5, 3, 10) and put them into a vector like:
```cpp
vector<int> costs = {3, 7, 5};
```
Then we sort this list to get:
```cpp
costs = {3, 5, 7}
```


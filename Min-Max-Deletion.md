# Min Max Deletion
## Language: C++; Time Complexity: O(N); Concept: Greedy,  Suffix Maximum

We want to parry as many times as possible without losing the game. Since X >= A[i], losing the game is impossible.  
Since parrying costs one energy, we need to check if we can afford to lose that one energy point.  
If we want to parry at ith index we must check if X >= B[i] and if X-1 >= for all A[j] where j>i. (if X<A[j] dodging becomes impossible, chef loses the game.)

My initial approach to check for the max value of A after ith index was a bubble loop.
```cpp
        for (int i = 0; i < N; i++) {
            int maxVal = 0;
            for (int j = i + 1; j < N; j++) {
                maxVal = max(maxVal, A[j]);
            }
            maxFuture[i] = maxVal;
        }
```
 



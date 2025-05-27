# B. Skibidus and Ohio

## Language: Python 3

At first glance, the problem seemed simple- given a string, I had to repeatedly perform an operation that lets me replace one letter and delete the next if those two letters are the same, aiming to minimize the final string length.  

The operation itself sounded a bit confusing: "replace the first letter with any letter and remove the second" - which made me wonder what the best strategy could be. Initially, I thought the replacement letter might matter a lot, and I wasn’t sure how to simulate or track that efficiently.  

### Early Attempts (misstep, but helped me think):  
My first attempt was straightforward: I just tried to count pairs of equal consecutive letters and reduce the length by that count, like:

```python
s = input().strip()
length = len(s)
for i in range(1, length):
    if s[i] == s[i-1]:
        length -= 1
print(length)
```
But this approach was too naive. It didn’t handle the fact that after replacing one letter, new pairs could form, allowing further reductions. It only counted immediate pairs without simulating how the string evolves after operations.  

I realized I needed to simulate the process step-by-step, actually modifying the string.

### Deeper Analysis  

I paused to understand the core of the operation. Since I can replace the first letter in any pair with *any letter*, I have control to create pairs that help me remove even more characters.  

For example, if the string is "bcc", I can turn "cc" into "b" by replacing the first "c" with "b" and removing the second "c". This creates "bb", which itself is a pair I can shrink further.  

So the problem reduces to:  
**Repeatedly remove adjacent duplicates until none remain.**

This meant I no longer needed to guess or track replacement letters explicitly. The best replacements always let me collapse as many pairs as possible.  

To simulate this, I wrote a code that, in a loop, keeps removing adjacent duplicates until the string length stops changing:

```python
t = int(input())
for x in range(t):
    s = input().strip()
    
    while True:
        prev_len = len(s)
        if len(s) == 1:
            break
        s = ''.join([s[i] for i in range(1, len(s)) if s[i] != s[i-1]] + [s[-1]])
        if len(s) == prev_len:
            break
    
    print(len(s))
```
### Breaking Down 
```python
s = ''.join([s[i] for i in range(1, len(s)) if s[i] != s[i-1]] + [s[-1]])
```


| Part                             | Explanation                                                                                                                                                                                                                                      |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| s[i] for i in range(1, len(s)) | We're looping through the string starting from the second character (index 1) to the end. We skip index 0 because we always need to compare s[i] with the one before it (s[i-1]).                                                        |
| if s[i] != s[i-1]              | We're checking whether the current character is different from the one before it. If it's different we keep this character.                                                                  |
| [s[-1]]                        | We add the last character of the original string at the end of the new string to avoid accidentally dropping it. Otherwise, if we just loop from index 1 and conditionally keep characters, we’d lose the last one if it never got compared. |
| ''.join(...)                   | Finally, we join all the characters back together into a single string. This is the new s after one iteration.                                                                                                         |


- This builds a new string skipping letters that are the same as their previous letter (effectively removing duplicates).
- It repeats this process until the string can’t be shortened further.

I struggled a bit with the part where the code rebuilds the string by picking certain characters out of it in a single line. The key part was recognizing that in each iteration, I’m removing one letter from every pair of duplicates. Since the problem allows changing the letter, I don't have to worry about what letter stays, just that one letter from each pair disappears.  

This repeated collapsing reflects the optimal strategy - the string shrinks as much as possible because I can always choose to replace letters to enable more removals.



















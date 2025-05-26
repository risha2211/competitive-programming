# A. Skibidus and Amog’u
## Language: Python 3

Every singular noun in this language ends with "us", and to convert it to plural, I just needed to drop the "us" and add an "i" instead.

```python
t = int(input())

for x in range(t):
    singular = input().strip()
    print(singular[:-2] + 'i')
```

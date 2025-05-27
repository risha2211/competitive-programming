# B. Skibidus and Ohio

## Language: Python 3

At first glance, the question seemed simple: I had to minimize the string length by repeatedly collapsing adjacent equal characters, replacing one and removing the next. The operation sounded weird at first (replace + remove), but I quickly realized something important - it didn’t matter what letter I replaced with. The net effect of this operation was that two identical letters shrink to one. That's it.

The problem says:

“Choose an index i such that s[i] == s[i+1]. Replace s[i] with any lowercase letter. Then remove s[i+1] from the string.”

That sounds like two steps:

- Replace s[i] with any letter you want.

- Delete s[i+1].

Now here’s the main thing:

- Since I can replace s[i] with any letter, what’s stopping me from just making s[i] equal to s[i+1] before deleting s[i+1]?

- In fact, since they're already equal, you don't even need to replace anything. You can imagine the operation as: "two same letters become one".

Example:
Suppose s = "aa".

You’re allowed to:

Replace s[0] = 'a' with any letter — let's say 'x', 'b', or even leave it 'a'.

Then remove s[1].

So:

Replace s[0] with 'a' (no real change), remove s[1] → result = "a"

Replace s[0] with 'x', remove s[1] → result = "x"

But we want to minimize the string's length, not make it look different.

So the optimal move is to always just let "aa" → "a". That’s the shortest you can make it.

That’s why we don’t actually care about the "replace" part — as long as the two characters are equal, we just collapse them into one.

This led me to one core realization:

Any pair of identical adjacent letters can be reduced to a single letter, and I can keep doing this greedily as long as there are such pairs.



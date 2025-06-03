There are 3 energy crystals, numbered 1, 2, and 3.

Initially, all crystals have 0 energy.

Our goal is to charge each crystal to energy level (x).

Only one action can be performed at a time:

In one action, the energy level of any one crystal can be increased by any positive amount (freely chosen).

**Constraint (the tricky part):**

After every action, the following condition must hold:

For every pair of crystals \(i\) and \(j\), it must be true that:

\[
a_i \geq \left\lfloor \frac{a_j}{2} \right\rfloor
\]

where \(a_i\) and \(a_j\) are the current energy levels of the crystals.

This means:

No crystal can be significantly smaller than another.

For example, if one crystal has energy 20, then every other crystal must be at least \(\lfloor 20 / 2 \rfloor = 10\).

This condition must be satisfied after **every** action, not just at the end.

**Objective:**

Given a value \(x\), determine the minimum number of actions required to charge all three crystals to exactly \(x\), while always obeying the constraint.

**Example to Visualize:**

Let \(x = 4\), and name the crystals A, B, and C.

Start:  
A = 0, B = 0, C = 0

Now consider this (invalid) move:  
A = 4, B = 0, C = 0 → Invalid  
Because B = 0, and \(\lfloor 4 / 2 \rfloor = 2\), so B < 2

A better approach might be:

A = 1  
B = 1  
C = 1 → Rule satisfied

Then:  
A = 2  
B = 2  
C = 2 → Still balanced

And so on...

**Intuition:**

The constraint enforces balanced growth. No crystal can get too far ahead of the others.  
The challenge is to reach the target value \(x\) using as few actions as possible while maintaining this balance.

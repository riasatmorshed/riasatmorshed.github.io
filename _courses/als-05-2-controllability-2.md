---
title: "05.2 Controllability 2"
collection: courses
permalink: /courses/applied-linear-systems/05-2-controllability-2/
---

Once we get the basic intuition from [05.1 Controllability 1](/courses/applied-linear-systems/05-1-controllability-1/), how do we know that if a system is controllable?
There are couple of ways actually to do this. They are as follows:

## First: Using MATLAB and LTI Object
We need to create an LTI object using state-space realization [03.1 Creating a LTI Object in MATLAB - Part 1](/courses/applied-linear-systems/03-1-creating-a-lti-object-in-matlab-part-1/) and [03.2 Creating a LTI Object in MATLAB - Part 2 (Conversion)](/courses/applied-linear-systems/03-2-creating-a-lti-object-in-matlab-part-2-conversion/)

Then use the following code-snippet
``` octave
sys = ss(A,B,C,D)
Q = ctrb(sys)
```

## Second: Create the Q matrix and determine the rank of the matrix

You can form the controllability matrix by yourself with the following formula
$$
Q = \mathbf{ \begin{bmatrix}B & AB & A^2B & ... & A^{N-1}B \end{bmatrix}}
$$
$Q$ is of $N\times M$
$B$ is of $N \times M$
and rest of the elements of $Q$ matrix is of $N \times M$
``` octave
rank_of_Q = rank(Q)
```

## Third: Controllability Grammian (TODO)


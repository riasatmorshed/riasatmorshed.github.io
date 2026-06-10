---
title: "03.2 Creating a LTI Object in MATLAB - Part 2 (Conversion)"
collection: courses
permalink: /courses/applied-linear-systems/03-2-creating-a-lti-object-in-matlab-part-2-conversion/
---

# State-Space to Transfer Function
## Method 1 (Analytical)

Say, you know $A,B,C,D$ matrix. Just define a symbolic s and then use the following formula:

$$G(s) = C(sI-A)^{-1}B+D$$

``` octave
syms s
m,n = size(A)
ident_mat = eye(m)
G(s) = C*inv((s*ident_mat-A))B+D
```
## Method 2 (State-Space to Transfer Function)
```matlab
[num, den] = ss2tf(A,B,C,D)
sys_tf = tf[num,den]
```


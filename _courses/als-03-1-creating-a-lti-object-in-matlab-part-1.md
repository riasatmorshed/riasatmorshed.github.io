---
title: "03.1 Creating a LTI Object in MATLAB - Part 1"
collection: courses
permalink: /courses/applied-linear-systems/03-1-creating-a-lti-object-in-matlab-part-1/
---

There are many ways to create an LTI object in MATLAB. However, the most conventional are two methods. 
1. State-Space to LTI
2. Transfer Function to LTI
**In my experience, if you don't have both the equations- only the ODE, always go for constructing *Transfer Function* first and then convert it to LTI**.
Reason is if you don't know the exact mapping of $y=Cx+Dy$ then you might end up with wrong result. 

# Method 1 (Transfer Function to LTI)
## Example
$\ddot{y}+10(\dot{y}-\dot{u})+26(y-u)=42\dot{u}+442u$

Now, if you take the Laplace transform and rearrange this equation it'll take the form: 
$$\ddot{y}+10\dot{y}+26y = 52\dot{u}+468u$$
$$s^y + 10s y + 26y = 52s u + 468u$$
$$\rightarrow (s^2+10s+26)y = 52(s+9)u $$
$$\rightarrow \frac{y}{u} = \frac{52(s+9)}{s^2+10s+26}$$
```matlab
num = 52 * [1 9];
den = [1 10 26];
P1_tf = tf(num, den)
P1_ss = ss(P1_tf)
```

# Method 1 (State-Space to LTI)

This is the mistake I made with the above example. What I did is I took the ODE:
$$\ddot{y}+10\dot{y}+26y = 52\dot{u}+468u$$
And my state-space representation was:

$$A = \begin{bmatrix} 0 & 1 \\ -26 & -10 \end{bmatrix} B = \begin{bmatrix}0&0\\468 & 52 \end{bmatrix}$$ 
What I assumed was $C=\begin{bmatrix}1&0\end{bmatrix}$ because my logic was: Typically, for a SISO system, the output y=x1, which corresponds to the first state variable, that is $y=Cx$.
==But this is wrong==! And my code was the following:

```matlab
clear; clc; close all;

A = [0 1;-26 -10];

B = [0 0;468 52];

% Typically, for a SISO system, the output y=x1, which corresponds to the

% first state variable, not the identity matrix for C

C = [1 0];

D = []; %since it's a SISO system

ss_obj = ss(A,B,C,D);

transferFunc = tf(ss_obj)
```
### Again, this is wrong!


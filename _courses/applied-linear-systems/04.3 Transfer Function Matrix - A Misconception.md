---
title: "04.3 Transfer Function Matrix - A Misconception"
collection: courses
permalink: /courses/applied-linear-systems/04-3-transfer-function-matrix-a-misconception/
---

From [03.1 Creating a LTI Object in MATLAB - Part 1](/courses/applied-linear-systems/03-1-creating-a-lti-object-in-matlab-part-1/), there might be a misconception that transfer function, $\mathbf{H}$ is a single polynomial. Something like the following:

$$H(s) = \frac{52(s+9)}{s^2+10s+26}$$

And that is true- but for a SISO (Single Input-Single Output) system.

If you think of a MIMO system, then transfer function, $H(s)$ is not a single polynomial alone. This is a matrix, $\mathbf{H(s)}$. For instance, look up the following MIMO system from [05.1 Controllability 1](/courses/applied-linear-systems/05-1-controllability-1/):

## MIMO System
$$ \begin{bmatrix}
\dot{x_1}\\
\dot{x_2}\\
\dot{x_3}
\end{bmatrix}= \begin{bmatrix}
-1 & 0 & 0 \\
0 & -2 & 1\\
0 & 2 & -2
\end{bmatrix} \begin{bmatrix}
x_1\\
x_2\\
x_3
\end{bmatrix} + \begin{bmatrix}
0&1\\
1&0\\
1&0
\end{bmatrix} \begin{bmatrix}
u_1\\
u_2
\end{bmatrix}
$$
$$[y] =\begin{bmatrix}1&0&-1 \end{bmatrix} \begin{bmatrix} x_1\\x_2\\x_3 \end{bmatrix}+\begin{bmatrix} 0&0\end{bmatrix}\begin{bmatrix}u_1\\u2 \end{bmatrix}$$


## Explanation

In this system, we have $M = 2$ meaning, 2 inputs, right? So, if you think in terms of a SISO system, you will be tripped up, like, there should be 2 $u$'s, right?  $$\frac{y(s)}{u(s)} = \frac{52(s+9)}{s^2+10s+26}$$ Therefore, the only explanation is the input-output relationship is like the following:
$$y = \begin{bmatrix}H_{11}(s) & H_{12}(s) \end{bmatrix} \begin{bmatrix} u_1 \\ u_2 \end{bmatrix}$$
So there are two transfer functions! You interpret it as:  $H_{11}$ is transfer path from $u_1$ to $y$ and $H_{12}$ is transfer path from $u_2$ to 1 only.

## Solution to the State-Space System Above

$$H_{11}(s) = \frac{2}{s^3+8s^2+19s+12}$$
$$H_{12}(s)=\frac{2s^2+10s+10}{s^3+8s^2+19s+12}$$
Now, typically they share the same poles but that's another discussion (TODO)

## MATLAB Technique

#### Problem Statement: If we have a MIMO system, and we would like to extract the sub-system only for the first input

``` octave
RC = 1;
A = (1/RC)*[-3 1 0; 1 -2 1; 0 1 -3];
B = (1/RC)*[2 0; 0 0; 0 2];
C = [0 0 1];
D = [0 0];
ss_sys = ss(A,B,C,D);


%% Now this ss_sys has two transfer function, right? H_11 and H_12
%% So to access this TF you need to index 

ss_sys11 = ss_sys(1,1);
ss_sys12 = ss_sys(1,2);
```

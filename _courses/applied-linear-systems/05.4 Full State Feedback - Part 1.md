---
title: "05.4 Full State Feedback - Part 1"
collection: courses
permalink: /courses/applied-linear-systems/05-4-full-state-feedback-part-1/
---

We start with a state-space system where we have $A,B,C,D$ defined, right? We can refer to the MIMO system mentioned in [04.3 Transfer Function Matrix - A Misconception](/courses/applied-linear-systems/04-3-transfer-function-matrix-a-misconception/).

So basically, for an open loop, it goes like this:

$$\begin{aligned}\dot{x} = Ax + Bu \\ y = Cx +Du \end{aligned}$$

Now, how would you know that this is open loop? We know this because when we close the loop using full-state feedback, we define our control law to be $u=-Gx$. And if we substitute this equation into the state-space system above, the state-space system takes the following form:

$$\dot{x} = [A-BG]x $$

This tells us that the loop is closed. Anyway...

The point is that full-state feedback means the $\mathbf{G}$ matrix is an $M\times N$ matrix that applies to all the states, meaning all the elements of $\mathbf{x}$:

$$\begin{bmatrix} x_1 \\ x_2 \\ ... \\ x_n \end{bmatrix}$$

But the question is: how do I get the $G$?

One method is called pole placement. Now, what is pole placement? By looking at the poles of the system, or to be more precise, their positions in the s-plane, we can assume the response of a system. So, if we want our system to behave in a certain way, we can choose closed-loop poles that match that behavior. More on that in this [03.6 Pole Placement (Const Damping and Const Freq Line) s-plane](/courses/applied-linear-systems/03-6-pole-placement-const-damping-and-const-freq-line-s-plane/) note.

Then we use MATLAB's `place(A,B,desired_closed_loop_poles)` function to obtain the $G$ matrix. MATLAB tells us what gain values, or what $G$ matrix, we need to make the closed-loop system achieve those desired closed-loop poles.

#### Note

Above, I said that full-state feedback gives me a $G$ matrix of size $M\times N$, which is applied to all the elements of $\mathbf{x}$:

$$\begin{bmatrix} x_1 \\ x_2 \\ ... \\ x_n \end{bmatrix}$$

We can also define it in a way where I want only states $x_2, x_4$ to be affected by my control gain. More on that in L12 of Applied Linear System class.


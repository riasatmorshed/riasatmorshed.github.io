---
title: "06.3 Observer (State Estimator) and Augmented System"
collection: courses
permalink: /courses/applied-linear-systems/06-3-observer-state-estimator-and-augmented-system/
---

We have cleared up the confusion regarding the [06.1 Luenberger Observer (State Estimation) - Full State Feedback - 2](/courses/applied-linear-systems/06-1-luenberger-observer-state-estimation-full-state-feedback-2/). By the way, observer means state estimator!

Now, in L14, professor showed an augmented system for real state, $x$ and $\hat{x}$.  Look up the L14S29 for the expression:

$$
\begin{bmatrix}\dot{x} \\ \dot{\hat{x}}\end{bmatrix} = \begin{bmatrix} A & 0 \\ KC & \hat{A}-K\hat{C}\end{bmatrix} \begin{bmatrix} x \\ \hat{x} \end{bmatrix}+ \begin{bmatrix}B \\ \hat{B}+K(D-\hat{D}) \end{bmatrix} u
$$

$$
\begin{bmatrix} y \\ \hat{y} \end{bmatrix} = \begin{bmatrix} C & 0 \\ 0 & \hat{C} \end{bmatrix} \begin{bmatrix}x \\ \hat{x} \end{bmatrix} + \begin{bmatrix} D \\ \hat{D} \end{bmatrix} u
$$

> Now, you may ask why do I need augmented system?
> 	Because observer/estimator use the output from the plant, right? And then use that to correct estimated state, $\hat{x}$. So, in that way, $x$ and $\hat{x}$ kind of grows/evolves together. So, if we build an LTI object, we can use `initial` function to plot for the evolution of both $x$ and $\hat{x}$ 
> 	
> 	Also because we will be developing an augmented system including my control input later [06.4 Augmented System - 2 with Control Command](/courses/applied-linear-systems/06-4-augmented-system-2-with-control-command/) 
> 
> Second question: In real life, we won't have real $x$, right? 
> 	Yes, we don't. In real life, we identify the system. By system, I mean, $A, B, C, D$ matrix and we don't have real states.
> 
> Third Question: Then in my ALS final project did I have real states, $x$. 
> 	Yes, I do. Because I developed the state-space system from first principles, like equation of motions. Therefore, I had access to real $A,B,C,D$ matrix and MATLAB was simulating the state-spaces system that I developed from first principles using `lsim()`.
> 	
> 	However, when I do system-ID, I may come up with $A,B,C,D$ matrix that i obtained by system id of an experiment. i can give that to MATLAB and say that this is my real state! But, when I develop my model from first principles my states, $x$ corresponds to physical states, like velocity, position and so on.
> 	
> 	Whereas, states obtained from system ID might not be corresponding to "real/physical" states!

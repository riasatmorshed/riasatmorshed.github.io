---
title: "02.4 Controller or Compensator Design"
collection: courses
permalink: /courses/applied-linear-systems/02-4-controller-or-compensator-design/
---

When we are adding a controller/compensator into our system (by system, I mean, the state-space with the observer and with the control gains), what is the transfer function of that controller? By the way, a **compensator** just means the **controller block** that sits between the measured plant output and the plant input.
## But why would we want a transfer function for controller or compensator?

> Because once the observer-based controller is written as its own dynamic system, we can study the **controller itself** in the frequency domain.
> 
> That lets us check things like controller gain, bandwidth, phase/magnitude behavior, and robustness margins. It is not for simulating the whole closed-loop response directly; it is for understanding what the controller block is doing.

We have derived substituting $\mathbf{\hat{y}}$ and $u = -Gx$ into the [06.1 Luenberger Observer (State Estimation) - Full State Feedback - 2](/courses/applied-linear-systems/06-1-luenberger-observer-state-estimation-full-state-feedback-2/) state equation, For observer-based feedback:


$$
\mathbf{\dot{\hat{x}}} = \begin{bmatrix}\mathbf{\hat{A}-\hat{B}G-K\hat{C}+K\hat{D}G} \end{bmatrix} + Ky
$$

So we have the state equation but what about the output equation? we know the following:
$$  
\text{plant output } y \rightarrow \boxed{\text{compensator/controller}} \rightarrow \text{plant input } u  
$$
Using that information, we can develop a state-space formulation for the controller alone, which is as follows!
$$
\begin{align} \mathbf{\dot{\hat{x}}} &= \begin{bmatrix}\mathbf{\hat{A}-\hat{B}G-K\hat{C}+K\hat{D}G} \end{bmatrix} + Ky \\
u &= -\mathbf{G\hat{x}+0y}

\end{align}
$$

Now compare with generic state-space form:
$$  
\dot{x}_c=A_cx_c+B_cr  
$$
$$  
y_c=C_cx_c+D_cr  
$$

| For the **compensator**, the internal state is | the compensator input is the measured plant output | and the compensator output is the plant control input |
| :--------------------------------------------: | -------------------------------------------------- | ----------------------------------------------------- |
|                 $x_c=\hat{x}$                  | $r=y$                                              | <br>$y_c=u$                                           |

So:
$$ 
A_c=A-BG-KC+KDG  
$$
$$  
B_c=K  
$$
$$  
C_c=-G  
$$
$$  
D_c=0  
$$

That is why your professor said **(C) is like (-G)** and **(D=0)**. The output equation of the compensator is:

$$  
u=-G\hat{x}  $$

The key point: **(u) is not "output (y)" of the plant. It is the output of the compensator.** Then that same signal (u) becomes the **input to the plant**.

So there are two systems:

| System                 | Input | Output |
| ---------------------- | ----- | ------ |
| Plant                  | (u)   | (y)    |
| Compensator/controller | (y)   | (u)    |

That is the loop.

And no, "compensator/controller" does **not by itself mean closed-loop system**. It is one block. When you connect it with the plant so that plant output (y) feeds the compensator and compensator output (u) feeds the plant, then the **whole combined system** becomes closed-loop.

This is exactly why L15/S10 describes the output feedback compensator as a dynamic state-space system whose input is (y) and whose output is (u).

And then you can derive a transfer function $H(s)$ from that! 
$$  
H_c(s)=-G(sI-A+BG+KC-KDG)^{-1}K  
$$

Once you have a transfer function for the controller alone, you can obtain Bode Plot, right? 
### So in the bode plot, when you are plotting magnitude of the $H(s)$ of the controller against a frequency sweep, what are these frequency correspond to?


Practically, it answers:

> If the plant output/measurement (y) contains oscillation/noise/disturbance at frequency ($\omega$), how strongly will the controller convert that into control effort (u)?

So yes, it can correspond to excitation/disturbance frequency, but more generally it is the frequency of any signal entering the controller: motion, sensor noise, vibration, measurement fluctuation, etc.

High magnitude at high frequency means the controller may strongly amplify high-frequency measurement noise, causing large/fast control effort. That is why L15 warns that increasing observer convergence rate increases compensator gain and bandwidth.

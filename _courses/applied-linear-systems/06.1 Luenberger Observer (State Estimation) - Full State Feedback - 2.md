---
title: "06.1 Luenberger Observer (State Estimation) - Full State Feedback - 2"
collection: courses
permalink: /courses/applied-linear-systems/06-1-luenberger-observer-state-estimation-full-state-feedback-2/
---

From [05.4 Full State Feedback - Part 1](/courses/applied-linear-systems/05-4-full-state-feedback-part-1/), we know that control gain, $G$, is applied to all the states, right? But in practice, we typically do not have all the states. So we estimate them. Now, the question is: how do we estimate them?

We know a typical state-space system looks like this:

$$\begin{aligned}\dot{x} = Ax + Bu \\ y = Cx +Du \end{aligned}$$

But we do not know $x,A,B,C,D$ perfectly, right? So we start by saying that our estimates for them are $\hat{x},\hat{A},\hat{B},\hat{C},\hat{D}$. Using this, we can write our estimated state-space system as:

$$\begin{aligned}\dot{\hat{x}} = \hat{A}\hat{x} + \hat{B}u \\ \hat{y} = \hat{C}\hat{x} +\hat{D}u \end{aligned}$$

So with our estimated quantities, we can get an **estimated $\hat{y}$**, right? But how do we correct our estimation? We use a predictor-corrector idea. We correct our prediction with:

$$\dot{\hat{x}} = \hat{A}\hat{x} + \hat{B}u + K(y-\hat{y})
$$

### But now the question is how do we get $K$?

After a bit of mathematical manipulation with the formulation (for details, refer to L13), we see that this $K$ is determined by the $A$ and $C$ matrices (*with the caveat that we assume a perfect plant model*). But how do we get the numerical value of $K$?

#### Interestingly, this seems like a [05.4 Full State Feedback - Part 1](/courses/applied-linear-systems/05-4-full-state-feedback-part-1/) problem - something like determining $G$ values. How so?

See, our estimated state-space system works if we can guarantee that our estimated states converge faster than the real states, right? And this convergence depends on the **poles** of our estimated system. But can we make the **poles** of our estimated system go faster? Yes, we can. This is more like a [05.4 Full State Feedback - Part 1](/courses/applied-linear-systems/05-4-full-state-feedback-part-1/) problem.

We use the same `place` function in MATLAB. But instead of using `place(A,B,desired_closed_loop_poles)`, we use `place(A,C,desired_closed_loop_poles)`. Now, how do we place our poles? For that, we need the techniques from [03.6 Pole Placement (Const Damping and Const Freq Line) s-plane](/courses/applied-linear-systems/03-6-pole-placement-const-damping-and-const-freq-line-s-plane/).


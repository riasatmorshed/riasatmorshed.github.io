---
title: "07.4 Wrapping Up - 1"
collection: courses
permalink: /courses/applied-linear-systems/07-4-wrapping-up-1/
---

# Summary

1. We have come a long way from the open-loop plant [01.1 Basics of Open Loop](/courses/applied-linear-systems/01-1-basics-of-open-loop/) to the closed-loop plant [02.2 Closed Loop System with Feedback Control](/courses/applied-linear-systems/02-2-closed-loop-system-with-feedback-control/).

2. But we typically do not have access to the states. By states, I mean the $x$ vector itself, like the numerical value of the $x$ vector. I am not referring to the $A,B,C,D$ matrices. Those are the model, and they are obtained either from first principles or from system ID.

   Anyway, since we do not have direct information about the states (again, the $x$ vector), we use an observer to estimate the states: [06.1 Luenberger Observer (State Estimation) - Full State Feedback - 2](/courses/applied-linear-systems/06-1-luenberger-observer-state-estimation-full-state-feedback-2/).

3. And with the closed loop, the control law [02.4 Controller or Compensator Design](/courses/applied-linear-systems/02-4-controller-or-compensator-design/), and the observer, we have built an augmented system that can give us the response of a plant/system.

---

# To Recap

1. The way we closed the loop is that we substituted the control law $u = -Gx$ into the open-loop system. That gave us the $\dot{x}$ equation, that is, the state-space equation for a closed-loop system, right? That equation tells us how the **states** evolve, and the $y$ equation tells us how the **output** evolves.

2. For the observer equation, we used a predictor-corrector system where we used the output, $y$, and compared it with our *estimated* output, $\hat{y}$. Then we calculated the *gain* ($K$), which looks awfully similar to a feedback controller problem, right?

   So now, we needed to *augment* the system so that my new state-space equation has not just $\dot{x}$, but rather $\begin{bmatrix}\dot{x} \\ \dot{\hat{x}} \end{bmatrix}$. However, we wanted our observer to reach steady state faster than the original plant, right?

   > Now, that is defined by the poles. The eigenvalues of the $A$ matrix define the poles, and if they are farther into the left-half plane, they reach convergence faster.
   >
   > So typically what we did is we calculated the closed-loop poles and took a multiple, like $1/1.5/2/5$, of those closed-loop poles so that my observer has faster convergence.
   >
   > We used MATLAB's `place()` function so that we can calculate $K$. Basically, we are asking MATLAB: to achieve these poles, what kind of *"force"* do I need? And that *"force"* is what $K$ is!

3. Finally, we added [07.1 Integral Control (LQR) - Part 1](/courses/applied-linear-systems/07-1-integral-control-lqr-part-1/) into the system above. We also derived a transfer function for the controller alone so that we can study the behavior of the controller separately: [02.4 Controller or Compensator Design](/courses/applied-linear-systems/02-4-controller-or-compensator-design/).

   Anyway, we again used MATLAB's `place()` function and used the whole augmented matrix, the one we saw in [07.2 Integral Control (LQR) - Part 2](/courses/applied-linear-systems/07-2-integral-control-lqr-part-2/), to get the *gain* value ($G$). Now, you may ask: we again needed to give it some poles, right? And we are asking the same question as step 2: how much $G$ do I need to get those poles?

> But how did we do that?
>
> We did it in an iterative way. Like, we observed the response, such as "Settling Time" and "Control Effort", and based on that observation we changed our poles. Do we need to move them farther left or farther right? To get intuition for that, we can refer to [03.6 Pole Placement (Const Damping and Const Freq Line) s-plane](/courses/applied-linear-systems/03-6-pole-placement-const-damping-and-const-freq-line-s-plane/).

---

# Last Question

### Without this manual iterative process, is there any other way to know the **BEST** $G$ value to use?

> That is the question that optimal control answers. But how do we do that?
>
> We create a quadratic function and basically solve that quadratic cost function equation to get the optimal $G$. In this process, we solve the Riccati equation. The formation of that is in 07.5 Draft - Wrapping Up - 2.


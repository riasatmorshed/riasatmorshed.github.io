---
title: "06.2 Luenberger Observer - 2"
collection: courses
permalink: /courses/applied-linear-systems/06-2-luenberger-observer-2/
---

### MATLAB Implementation of Luenberger Observer and Why this observer problem looks like a [05.4 Full State Feedback - Part 1](/courses/applied-linear-systems/05-4-full-state-feedback-part-1/)

From [06.1 Luenberger Observer (State Estimation) - Full State Feedback - 2](/courses/applied-linear-systems/06-1-luenberger-observer-state-estimation-full-state-feedback-2/) we know that our estimated state-space system will work if we can guarantee that our estimated states converged faster than the real states, right? And this convergence will depend on the **poles** of our estimated system. But can we make the **poles** of our estimated system go faster? Yes we can, this is more like [05.4 Full State Feedback - Part 1](/courses/applied-linear-systems/05-4-full-state-feedback-part-1/) problem. We will use the same `place` function of MATLAB. But instead of using `place(A,B,desired_closed_loop_poles)`, we will be using `place(A,C,desired_closed_loop_poles)`. Now, how do we place our poles? For that, we will need the techniques from the [03.6 Pole Placement (Const Damping and Const Freq Line) s-plane](/courses/applied-linear-systems/03-6-pole-placement-const-damping-and-const-freq-line-s-plane/). 

#### Always use transpose while calculating for the observer

``` octave
K = place(A',C',obspoles) % obs = observer
```

---
### But for that we need to know the poles of the "model" or the system, right?
> Someone might ask, if we know the system, why do we need the observer to begin with?

By "model", we mean $A,B,C,D$ matrices that come from equation of motion. And using $\hat{y} = \hat{C}\hat{x}+\hat{D}u$, we might obtain whatever's my sensor is measuring, say, $x_2$. For more clarification, refer to [04.2 Intuition (Mapping) of State-Space Realization](/courses/applied-linear-systems/04-2-intuition-mapping-of-state-space-realization/). So, we know $x_2$ but we don't know the numerical values for $x_1$, $x_3$ and so on. And Luenberger Observer calculates the states themselves, meaning, $x_1, x_2$ and so on.

---


[05.3 Draft - Why Observability and Controllability are Dual Problems](/courses/applied-linear-systems/05-3-draft-why-observability-and-controllability-are-dual-problems/)

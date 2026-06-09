---
title: "07.1 Integral Control (LQR) - Part 1"
collection: courses
permalink: /courses/applied-linear-systems/07-1-integral-control-lqr-part-1/
---

We have come a long way from open-loop plant [01.1 Basics of Open Loop](/courses/applied-linear-systems/01-1-basics-of-open-loop/) to closed-loop plant [02.2 Closed Loop System with Feedback Control](/courses/applied-linear-systems/02-2-closed-loop-system-with-feedback-control/).

But we typically do not have access to the states. By states, I mean the $x$ vector itself, like the numerical value of the $x$ vector. I am not referring to the $A,B,C,D$ matrices. Those are the model, and they are obtained either from first principles or from system ID.

Anyway, since we do not have direct information about the states (again, the $x$ vector), we use an observer to estimate the states: [06.1 Luenberger Observer (State Estimation) - Full State Feedback - 2](/courses/applied-linear-systems/06-1-luenberger-observer-state-estimation-full-state-feedback-2/).

And with the closed loop, the control law [02.4 Controller or Compensator Design](/courses/applied-linear-systems/02-4-controller-or-compensator-design/), and the observer, we have built an augmented system that can give us the response of a plant/system.

[07.3 Draft - Summary Equations for Closed Loop, Observer, Controller](/courses/applied-linear-systems/07-3-draft-summary-equations-for-closed-loop-observer-controller/)

---

But how did we end up with an integral controller? And how does reference tracking come into play?

> Integral control comes from the reference tracking problem. For instance, say you want your output $\mathbf{y}$ to be a certain way. So then you calculate the error, right?

$$e(t) = r(t)-y(t)$$

> So you have an error vector. You take it and sum it up to get the integrated error, right? Something like this:

$$x_I(t) = \int e(\tau)d\tau$$

> We can understand why we integrate the error, but why do we say that it is equal to $\mathbf{x_I}$?
>
> Because we wanted to create a controller state. Why?

**Because output (y) is determined by the plant states (x), and tracking error depends on (y), we add a controller state ($\mathbf{x_I}$) to remember accumulated tracking error and help drive (y) to the reference.**

> Also, when you say **integration**, that essentially means a $\frac{1}{s}$ term in the frequency/Laplace domain. Therefore, the integral part has its own dynamics.

Anyway, once we have our controller state, $\mathbf{x_I}$, we define its derivative so that it can be augmented into a state-space system:

$$\mathbf{\dot{x_I}} =\mathbf{e(t)} = \mathbf{r(t)-\mathbf{y(t)}}$$

---

> But why would you want that $\mathbf{x_I}$ thing anyway?
>
> Because we are planning to use a control law like this:

$$ \mathbf{u(t)=-\mathbf{G_0 x(t)-G_I x_I(t)}}
$$


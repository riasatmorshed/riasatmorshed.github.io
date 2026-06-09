---
title: "03.4 Impulse Response Function Plotting"
collection: courses
permalink: /courses/applied-linear-systems/03-4-impulse-response-function-plotting/
---

TODO: HW from Applied Linear System

If we have a second order system- in other words, if you have a second order transfer function, you can extract the poles of the system from it. 

Poles are the property that dictates system's ability to reach steady-state (Conversely, zeros have nothing to do with stability). By the way, poles are the ones that are roots of the denominator of the transfer function.

Anyway, say, 
> You have a transfer function.
> Extract the denominator from it
> Pass it through the `damp()` function [01.3 Natural Frequency, Poles, Damping (2nd Order System)](/courses/applied-linear-systems/01-3-natural-frequency-poles-damping-2nd-order-system/)
> This will give you time constant. 
> This "time constant" is what will dictate when your system will reach steady-state. Equation for time constant, $\tau=\frac{1}{\zeta\times\omega_n}$ [03.6 Pole Placement (Const Damping and Const Freq Line) s-plane](/courses/applied-linear-systems/03-6-pole-placement-const-damping-and-const-freq-line-s-plane/)
> So when you are plotting IRF, make sure that it is $4-5$ times the "time-constant"

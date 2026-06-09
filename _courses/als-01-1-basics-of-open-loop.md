---
title: "01.1 Basics of Open Loop"
collection: courses
permalink: /courses/applied-linear-systems/01-1-basics-of-open-loop/
---

## Derivation of P(s) - Second-Order System

$P(s)$ comes from the standard **mass-spring-damper** system:

$$m\ddot{x} + c\dot{x} + kx = F$$

Taking the Laplace transform (zero initial conditions):

$$ms^2X(s) + csX(s) + kX(s) = F(s)$$

$$\frac{X(s)}{F(s)} = \frac{1}{ms^2 + cs + k} = \frac{1/m}{s^2 + \frac{c}{m}s + \frac{k}{m}}$$

**Standard form substitution:**

- Natural frequency: $\omega_n = \sqrt{k/m}$
- Damping ratio: $\zeta = \frac{c}{2\sqrt{km}}$

This gives: $$P(s) = \frac{\omega_n^2}{s^2 + 2\zeta\omega_n s + \omega_n^2}$$

The $\omega^2$ in the numerator ensures **unity DC gain** (when $s=0$, $P(0)=1$), which is the standard normalized form for second-order systems. For details, refer to [01.2 DC Gain Explained](/courses/applied-linear-systems/01-2-dc-gain-explained/)

Then from open loop, we will continue to [02.1 Basics of Closed Loop](/courses/applied-linear-systems/02-1-basics-of-closed-loop/)


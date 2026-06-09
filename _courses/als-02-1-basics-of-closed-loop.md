---
title: "02.1 Basics of Closed Loop"
collection: courses
permalink: /courses/applied-linear-systems/02-1-basics-of-closed-loop/
---

## What is an Open-Loop Plant?

An **open-loop plant** $P(s)$ is simply the transfer function of the system you want to control, without any feedback. It describes how the system naturally responds to inputs.

In your case: $$P(s) = \frac{\omega^2}{s^2 + 2\zeta\omega s + \omega^2}$$

This is a standard **second-order system** (like a mass-spring-damper), where:

- $\omega$ is the natural frequency
- $\zeta$ is the damping ratio

## Unity Negative Feedback Configuration

Here's the standard block diagram:

```
        +        +------+       +------+
r(s) --->(sum)-->| C(s) |------>| P(s) |----+----> y(s)
        - ^      +------+       +------+    |
          |                              |
          +------------------------------+
```

Where:

- $r(s)$ = reference input
- $y(s)$ = output
- $C(s)$ = compensator (what we're solving for)
- $P(s)$ = plant

## Deriving the Closed-Loop Transfer Function

The **loop transfer function** is: $L(s) = C(s) \cdot P(s)$

For unity negative feedback, the **closed-loop transfer function** is:

$$T(s) = \frac{y(s)}{r(s)} = \frac{C(s)P(s)}{1 + C(s)P(s)}$$

**Why?** Let's derive it from the block diagram:

1. At the summing junction: $e(s) = r(s) - y(s)$
2. Through the compensator and plant: $y(s) = C(s) \cdot P(s) \cdot e(s)$
3. Substituting: $y(s) = C(s)P(s)[r(s) - y(s)]$
4. Expanding: $y(s) = C(s)P(s)r(s) - C(s)P(s)y(s)$
5. Collecting $y(s)$ terms: $y(s)[1 + C(s)P(s)] = C(s)P(s)r(s)$
6. Therefore: $\boxed{T(s) = \frac{y(s)}{r(s)} = \frac{C(s)P(s)}{1 + C(s)P(s)}}$

The reason it is called **unity negative feedback** is because we are subtracting the output from the reference. For instance, at step 3:

$e(s)=r(s)-1\times y(s)$, where gain = 1. That is the "unity" part, and the subtraction is the "negative feedback" part.


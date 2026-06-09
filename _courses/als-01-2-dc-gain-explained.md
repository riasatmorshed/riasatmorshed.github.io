---
title: "01.2 DC Gain Explained"
collection: courses
permalink: /courses/applied-linear-systems/01-2-dc-gain-explained/
---

**DC gain** is the steady-state output of a system when you apply a constant (DC) input. "DC" comes from electronics-direct current means zero frequency.

### Physically:
If you apply a constant force to a mass-spring-damper and wait forever, how far does it move? ***That ratio (output/input at steady state) is the DC gain.***

### Mathematically: 
Set $s = 0$ in the transfer function:

$$\text{DC gain} = P(0) = \lim_{s \to 0} P(s)$$

For your system [01.1 Basics of Open Loop](/courses/applied-linear-systems/01-1-basics-of-open-loop/): $$P(0) = \frac{\omega^2}{0 + 0 + \omega^2} = 1$$

This means a unit step input eventually produces a unit step output (no amplification or attenuation at steady state).

---

## Why It Matters

- **DC gain = 1**: Output tracks input perfectly at steady state
- **DC gain > 1**: System amplifies constant inputs
- **DC gain < 1**: System attenuates constant inputs
- **DC gain = infinity**: System has an integrator (type 1 or higher), output grows unbounded for step input
## MATLAB
### Method 1
MATLAB has a function `dcgain()`. Just pass a LTI object and it will give you a DC gain.  `dcgain(P1_ss)` and it will output 18 [03.1 Creating a LTI Object in MATLAB - Part 1](/courses/applied-linear-systems/03-1-creating-a-lti-object-in-matlab-part-1/) (`P1_ss`) is taken from here

### Method 2
You can also use `freqresp` function to get DC Gain. `freqresp` gives you the output at a particular frequency or for an array of frequency if you give it an **LTI Object**

```octave
DC_gain = freqresp(P1_ss, 2*pi*0) %always convert the input to radian.
```


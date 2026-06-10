---
title: "01.3 Natural Frequency, Poles, Damping (2nd Order System)"
collection: courses
permalink: /courses/applied-linear-systems/01-3-natural-frequency-poles-damping-2nd-order-system/
---

### Eigenvalues = Poles
**Explanation:** Eigenvalues and poles are the same thing! 

---
### Now, What is natural frequency?
> Absolute value of a complex eigenvalue (or, pole) is the natural frequency of a system.
> But if you have a real eigenvalue, then the concept of natural frequency is kind of meaningless because it just means
> > an exponential decay of growth
> > Or, it just means you have an overdamped system $\zeta>1$ 

## Example:

Say, you have a characteristic equation (not a random polynomial- a characteristic equation):
$$s^4-2.51327s^3-86.85252s^2-496.1s=0$$

### Method 1: From Eigenvalues
Since the above polynomial is a characteristic equation, so we can find its roots and those will be your **eigenvalues** (**or, poles**) and taking a modulus of those would be your natural frequency:

``` octave
s_coeff = [1 -2.51327 -86.85252 -496.1 0];
eigenVal_roots = roots(s_coeff);
for i = 1:length(eigenVal_roots)
	a = ~isreal(sorted_eigVal(i));
	if a == 1
		break
	end
end

natFreq = sqrt(real(sorted_eigVal(i))^2+imag(sorted_eigVal(i))^2)
```

### Method 2: Analytical (kind of)

We know that a second order system is
$$s^2+2\zeta \omega_n s+\omega_n^2 = 0$$
Therefore, the roots of that second order equation is:
$$s = -\zeta \omega_n \pm j\omega_n\sqrt{1-\zeta^2 }$$
See, this is a generic polynomial- not a characteristic equation. But this is the relation between the roots of a polynomial (not a characteristic equation) and natural frequency, $\omega_n$  along with damping ratio, $\zeta$

$$\begin{align}
Real Part of Root &= -\zeta \omega_n \\\\
Imaginary Part of Root &= j\omega_n\sqrt{1-\zeta^2}
\end{align}
$$


For the same problem MATLAB code is:

```matlab
s_coeff = [1 -2.51327 -86.85252 -496.1 0];
eigenVal_roots = roots(s_coeff);

syms omega_n zeta

natFreq_sym = solve([-zeta*omega_n==real(sorted_eigVal(i)),omega_n*sqrt(1-zeta^2)==imag(sorted_eigVal(i))],[omega_n,zeta]);

natFreq_pole = double(natFreq_sym.omega_n)
```

### Method 3: Purely MATLAB

Use MATLAB's `damp()` function

``` octave
[Wn,Z,P] = damp(eigenVal_roots)
```


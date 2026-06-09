---
title: "07.2 Integral Control (LQR) - Part 2"
collection: courses
permalink: /courses/applied-linear-systems/07-2-integral-control-lqr-part-2/
---

As we kind of defined why we needed a **controller state**, now we would like to incorporate that into our augmented system, right? [07.1 Integral Control (LQR) - Part 1](/courses/applied-linear-systems/07-1-integral-control-lqr-part-1/)

So, what does our equation look like:
$$\mathbf{\dot{x_I}} =\mathbf{e(t)} = \mathbf{r(t)-\mathbf{y(t)}}$$
and we know that $\mathbf{y} =\mathbf{Cx+Du}$, Therefore, $\mathbf{\dot{x_I}} =\mathbf{e(t)} = \mathbf{r-Cx-Du}$

And my state equation is:

$$ \mathbf{\dot{x}} =\mathbf{Ax+0\times x_I +Bu+0\times r + F\times w +0 \times \theta}
$$

If we arrange the equation above we get  the state-space representation along with **controller state**:
$$
\begin{bmatrix} \mathbf{\dot{x}} \\ \mathbf{\dot{x_I}} \end{bmatrix}
= \begin{bmatrix}A & 0 \\ -C &0 \end{bmatrix} \begin{bmatrix}\mathbf{x} \\ \mathbf{x_I} \end{bmatrix} + \begin{bmatrix}\mathbf{B} \\ \mathbf{-D} \end{bmatrix} \mathbf{u} + \begin{bmatrix}\mathbf{0} \\ \mathbf{I} \end{bmatrix} \mathbf{r} + \begin{bmatrix}\mathbf{F} \\ \mathbf{0} \end{bmatrix} \mathbf{w} + \begin{bmatrix}\mathbf{0} \\ \mathbf{0} \end{bmatrix} \mathbf{\theta}
$$

Now, this is our system and if we would like to close the loop, we will be using our control law which is:

$$ u(t)  = -\begin{bmatrix}\mathbf{G_0} & \mathbf{G_I} \end{bmatrix}\begin{bmatrix}\mathbf{x} \\ \mathbf{x_I} \end{bmatrix} = -\mathbf{G}\begin{bmatrix}\mathbf{x} \\ \mathbf{x_I} \end{bmatrix}
$$

If we replace this control law to the equation above, we get the closed loop representation:
$$
\begin{bmatrix} \mathbf{\dot{x}} \\ \mathbf{\dot{x_I}} \end{bmatrix}
= \begin{bmatrix}A-BG_O & -BG_I \\ -C+DG_0 &DG_I \end{bmatrix} \begin{bmatrix}\mathbf{x} \\ \mathbf{x_I} \end{bmatrix} + \begin{bmatrix}\mathbf{B} \\ \mathbf{-D} \end{bmatrix} \mathbf{u} + \begin{bmatrix}\mathbf{0} \\ \mathbf{I} \end{bmatrix} \mathbf{r} + \begin{bmatrix}\mathbf{F} \\ \mathbf{0} \end{bmatrix} \mathbf{w} + \begin{bmatrix}\mathbf{0} \\ \mathbf{0} \end{bmatrix} \mathbf{\theta}
$$

Anyway, but that does not end here. We want the 
1. Plant
2. Observer
3. Controller (Integral Control) 
All in the same plant. 

Our target is we will develop this augmented system by hand and then define matrices in MATLAB. Now, we can use MATLAB to spare us this hassle (But I did not follow that lecture in the class and hence forgot almost everything in that lecture!)

---

Now, if you recall the observer state equation (after substituting) from [07.3 Draft - Summary Equations for Closed Loop, Observer, Controller](/courses/applied-linear-systems/07-3-draft-summary-equations-for-closed-loop-observer-controller/) and from [06.3 Observer (State Estimator) and Augmented System](/courses/applied-linear-systems/06-3-observer-state-estimator-and-augmented-system/),

$$
\begin{bmatrix}\dot{\hat{x}} \end{bmatrix} = \begin{bmatrix}\hat{A}-K\hat{C} \end{bmatrix} \hat{x}+ \begin{bmatrix}KC \end{bmatrix}x+\begin{bmatrix}\hat{B}+K(D-\hat{D}) \end{bmatrix}u
$$
Now, if we augment that equation into the equations above we get the **ultimate equation** ready for full-state feedback to be used in MATLAB's `place()` function:

$$
\begin{gathered}
{\left[\begin{array}{c}
\dot{\mathbf{x}} \\
\dot{\mathbf{x}}_I \\
\dot{\hat{\mathbf{x}}}
\end{array}\right]=\left[\begin{array}{ccc}
\mathbf{A} & \mathbf{0} & \mathbf{0} \\
-\mathbf{C} & \mathbf{0} & \mathbf{0} \\
\mathbf{K C} & \mathbf{0} & \widehat{\mathbf{A}}-\mathbf{K} \widehat{\mathbf{C}}
\end{array}\right]\left[\begin{array}{c}
\mathbf{x} \\
\mathbf{x}_I \\
\hat{\mathbf{x}}
\end{array}\right]+\left[\begin{array}{c}
\mathbf{B} \\
-\mathbf{D} \\
\widehat{\mathbf{B}}+\mathbf{K}(\mathbf{D}-\widehat{\mathbf{D}})
\end{array}\right]\left[\begin{array}{ll}
-\mathrm{G}_0 & -\mathrm{G}_I
\end{array}\right]\left[\begin{array}{l}
\widehat{\boldsymbol{x}} \\
\mathbf{x}_I
\end{array}\right]+\left[\begin{array}{l}
\mathbf{0} \\
\mathbf{I} \\
\mathbf{0}
\end{array}\right] \mathbf{r}+\left[\begin{array}{l}
\mathbf{F} \\
\mathbf{0} \\
\mathbf{0}
\end{array}\right] \mathbf{w}+\left[\begin{array}{c}
\mathbf{0} \\
-\mathbf{I} \\
\mathbf{0}
\end{array}\right] \boldsymbol{\theta}} \\
{\left[\begin{array}{c}
\dot{\mathbf{x}} \\
\dot{\mathbf{x}} \\
\dot{\hat{\mathbf{x}}}
\end{array}\right]=\left[\begin{array}{ccc}
\mathbf{A} & \mathbf{0} & \mathbf{0} \\
-\mathbf{C} & \mathbf{0} & \mathbf{0} \\
\mathbf{K C} & \mathbf{0} & \widehat{\mathbf{A}}-\mathbf{K} \widehat{\mathbf{C}}
\end{array}\right]\left[\begin{array}{c}
\mathbf{x} \\
\mathbf{x}_I \\
\widehat{\mathbf{x}}
\end{array}\right]+\left[\begin{array}{cc}
-\mathbf{B} \mathrm{G}_0 & -\mathbf{B} \mathrm{G}_I \\
\mathbf{D} \mathrm{G}_0 & \mathbf{D G} \\
-\widehat{\mathbf{B}} \mathrm{G}_0-\mathbf{K}(\mathbf{D}-\widehat{\mathbf{D}}) \mathrm{G}_0 & -\widehat{\mathbf{B}} \mathrm{G}_I-\mathbf{K}(\mathbf{D}-\widehat{\mathbf{D}}) \mathrm{G}_I
\end{array}\right]\left[\begin{array}{l}
\widehat{\boldsymbol{x}} \\
\mathbf{x}_I
\end{array}\right]+\left[\begin{array}{l}
\mathbf{0} \\
\mathbf{I} \\
\mathbf{0}
\end{array}\right] \mathbf{r}+\left[\begin{array}{l}
\mathbf{F} \\
\mathbf{0} \\
\mathbf{0}
\end{array}\right] \mathbf{w}+\left[\begin{array}{c}
\mathbf{0} \\
-\mathbf{I} \\
\mathbf{0}
\end{array}\right] \boldsymbol{\theta}} \\
{\left[\begin{array}{c}
\dot{\mathbf{x}} \\
\dot{\mathbf{x}}_I \\
\dot{\hat{\mathbf{x}}}
\end{array}\right]=\left[\begin{array}{ccc}
\mathbf{A} & -\mathbf{B} \mathrm{G}_I & -\mathbf{B} \mathrm{G}_0 \\
-\mathbf{C} & \mathbf{D} \mathrm{G}_I & \mathbf{D} \mathrm{G}_0 \\
\mathbf{K C} & -\widehat{\mathbf{B}} \mathrm{G}_I-\mathbf{K}(\mathbf{D}-\widehat{\mathbf{D}}) \mathrm{G}_I & \widehat{\mathbf{A}}-\mathbf{K} \widehat{\mathbf{C}}-\widehat{\mathbf{B}} \mathrm{G}_0-\mathbf{K}(\mathbf{D}-\widehat{\mathbf{D}}) \mathrm{G}_0
\end{array}\right]\left[\begin{array}{c}
\mathbf{x} \\
\mathrm{x}_I \\
\widehat{\mathbf{x}}
\end{array}\right]+\left[\begin{array}{l}
\mathbf{0} \\
\mathbf{I} \\
\mathbf{0}
\end{array}\right] \mathbf{r}+\left[\begin{array}{c}
\mathbf{F} \\
\mathbf{0} \\
\mathbf{0}
\end{array}\right] \mathbf{w}+\left[\begin{array}{c}
\mathbf{0} \\
-\mathbf{I} \\
\mathbf{0}
\end{array}\right] \boldsymbol{\theta}}
\end{gathered}
$$

---
## MATLAB Implementation

Now, that you have the fully fledged equation we will be using 

``` octave
G = place(A',B', desired_poles)
```

Now, remember that this `G` has both $G_I$ and $G_0$. Now, $G_0$ has to be of $M\times N$ size and $G_I$ has to be of size $M \times P$. So to extract $G_I$ and $G_0$ from `G`:

``` octave
G0 = G(:,1:N);
GI = G(:,N+1:N+P);
```


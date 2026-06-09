---
title: "06.4 Augmented System - 2 with Control Command"
collection: courses
permalink: /courses/applied-linear-systems/06-4-augmented-system-2-with-control-command/
---

Once we complete [06.3 Observer (State Estimator) and Augmented System](/courses/applied-linear-systems/06-3-observer-state-estimator-and-augmented-system/), we would incorporate the control law into the augmented system.

## This is without control law
$$
\begin{bmatrix}\dot{x} \\ \dot{\hat{x}}\end{bmatrix} = \begin{bmatrix} A & 0 \\ KC & \hat{A}-K\hat{C}\end{bmatrix} \begin{bmatrix} x \\ \hat{x} \end{bmatrix}+ \begin{bmatrix}B \\ \hat{B}+K(D-\hat{D}) \end{bmatrix} u
$$

$$
\begin{bmatrix} y \\ \hat{y} \end{bmatrix} = \begin{bmatrix} C & 0 \\ 0 & \hat{C} \end{bmatrix} \begin{bmatrix}x \\ \hat{x} \end{bmatrix} + \begin{bmatrix} D \\ \hat{D} \end{bmatrix} u
$$
## If we add control law $u=-Gx$ to the augmented system above we will end up with the following


$$
\begin{bmatrix}\dot{x} \\ \dot{\hat{x}}\end{bmatrix} = \begin{bmatrix} A & -BG \\ KC & \hat{A}-K\hat{C}-\hat{B}G-K(D-\hat{D})G\end{bmatrix} \begin{bmatrix} x \\ \hat{x} \end{bmatrix}
$$

$$
\begin{bmatrix} y \\ \hat{y} \end{bmatrix} = \begin{bmatrix} C & -DG \\ 0 & \hat{C}-\hat{D}G \end{bmatrix} \begin{bmatrix}x \\ \hat{x} \end{bmatrix}
$$

---
## Extra


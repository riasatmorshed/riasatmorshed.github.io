---
title: "02.3 Gain Margin and Phase Margin"
collection: courses
permalink: /courses/applied-linear-systems/02-3-gain-margin-and-phase-margin/
---

## Let's say, you have a gain margin of $6+0.1 dB$, what does that mean?

> *This means your system's overall open-loop gain can increase by exactly 6 decibels before the closed-loop system goes unstable. In linear terms, 6 dB equates to a factor of roughly 2 (since $20log(2)=6$. This means your controller's gain could essentially double before your system starts oscillating out of control.*

> *This is simply the grading tolerance for your iterative "guess-and-check" process. Because finding the perfect sample rate for a mathematically exact 6.00000 dB margin is tedious, the problem is telling you that any sample rate that yields a gain margin anywhere between $5.9$ and $6.1$ is correct answer*

``` octave
[Gm, Pm, Wcg, Wcp] = margin(open_loop); %Wcg and Wcp is in rad/s
```

`Gm` = Gain Margin. You need to convert that to dB by `20log(Gm)`
`Wcg` = Gain Margin at phase cross-over frequency
> What is phase cross-over frequency?
> >*This is the frequency where the phase lag of your open-loop system drops to exactly -180 degrees.*
> 
> What is gain cross-over frequency?
> > *This is the frequency where the magnitude of your open-loop system crosses exactly 0 dB (a gain of 1)*



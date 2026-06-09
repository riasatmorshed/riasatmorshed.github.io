---
title: "03.3 State-Space Info from LTI Object"
collection: courses
permalink: /courses/applied-linear-systems/03-3-state-space-info-from-lti-object/
---

If you have an LTI object say, `H_sys`. And you would like to extract, `A`, `B` , `C` , `D` matrix, then use the following 

``` octave
[A, B, C,D] = ssdata(H_sys);
```


---
title: "Discrete-Time Transfer Functions Expansion: Almost There!"
date: 2025-06-13 19:05:00 +0200
categories: update
tags:
    - GSoC-2025
    - SymPy
---
Hello everyone, I'm in my second week of GSoC and I've almost finished writing the transfer function classes [#28115(Open)](https://github.com/sympy/sympy/pull/28115).

I proceeded as explained in my last update.

The design I used preserves retrocompatibility, practically no previous tests had to be changed.

I paid close attention to the compatibility of operations, series, parallel and feedback of systems.
To handle this, I wrote the `_check_compatibility` function and its decorator, `_compatibility_decorator`. These are responsible for checking if a list of systems are compatible (i.e., if they are all either continuous-time or discrete-time and if they share the same sampling time).
These functions have been particularly useful for the methods in the `Series`, `Parallel` and `Feedback` classes, as they frequently operate on multiple systems.

This design should also work fine with the `DTStateSpace` class, which I plan to add in the coming weeks.

I also added the discretization methods present in the module to the `DTTransferFunction` class. These methods convert continuous-time transfer functions to the discrete-time counterparts.
I plan to add more of them in the future, such as the [Padè approximation](https://en.wikipedia.org/wiki/Pad%C3%A9_approximant) for models with delays, as suggested by my mentor [@moorepants](https://github.com/moorepants).

In order to complete the "discretization" of transfer functions, I will need to write some tests to check compatibility, ensuring that every case is covered and to make minor changes to MIMO systems to ensure they work correctly with discrete-time systems.

What will remain is to write the discrete-time counterpart of the stability functions (`is_stable`, `get_asymptotical_stability_conditions`). However, I will do this at the end of the "discretization" process for all classes because it will require a significant amount of effort and I prefer to finish my exams first. I can spoil that I will probably use the [Jury stability criterion](https://en.wikipedia.org/wiki/Jury_stability_criterion), but more research is needed.
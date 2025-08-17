---
title: "Close to the end"
date: 2025-08-17 19:00:00 +0200
categories: update
tags:
    - GSoC-2025
    - SymPy
---

Hello everyone, the GSoC is getting close to the end.

Since the [last update](https://leomanga.github.io/update/july/), I went on vacation to the Canary Islands, because my mind needed to slow down a bit.

After recharging, I got back to SymPy and made good progress on the PR [#28265(open)](https://github.com/sympy/sympy/pull/28265), about the simplifications of the stability conditions for continuous-time systems.

After some discussions, we moved that function inside the `Poly` module and we decided that the best name for the function would be `routh-hurwitz-conditions` instead of `negative-real-part-conditions`, since this will also make it easier to name the discrete-time counterpart, which will probably be `schur-conditions`.

also found a way to further improve the simplification for the `EXRAW` domain, using `signsimp` and `factor_terms`.

Previous behaviour (from [last update](https://leomanga.github.io/update/july/)):
```python
In [1]: p = Poly(symbols("a:f"), x)
In [3]: for c in negative_real_part_conditions(p, x, domain = EXRAW): print(c) # algorithm for expressions
a*b > 0
-a*d + b*c > 0
b*(b*(a*f - b*e) - d*(a*d - b*c)) > 0
b*(a*d - b*c)*(f*(a*d - b*c)**2 + (a*f - b*e)*(b*(a*f - b*e) - d*(a*d - b*c))) > 0
b*f > 0
```
New behaviour:
```python
In [1]: p = Poly(symbols("a:f"), x, domain = EXRAW)
In [2]: for c in p.routh_hurwitz_conditions(): print(c)
a*b
-a*d + b*c
b*(b*(a*f - b*e) - d*(a*d - b*c))
-b*(f*(a*d - b*c)**2 + (a*f - b*e)*(b*(a*f - b*e) - d*(a*d - b*c)))
b*f
```
First of all, it’s easy to see how the usage changes, and that the `>` is no longer added by default. We made this choice to give the user more flexibility with the conditions.

Another difference in the output is the fourth printing. Now, the second condition `-a*d + b*c`, thanks to `signsimp`, is eliminated from the fourth.

In the next days I will work on some minor things to get this PR merged, and I will also have one of the last meetings where we’ll discuss the final steps for merging the discrete transfer functions and discrete state spaces PRs ([#28318(open)](https://github.com/sympy/sympy/pull/28318), [#28326(open)](https://github.com/sympy/sympy/pull/28326)).
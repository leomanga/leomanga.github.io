---
title: "Third Week Update"
date: 2025-06-13 12:30:00 +0200
categories: update
tags:
    - GSoC-2025
    - SymPy
---
Hello everyone, PR [#28115(Open)](https://github.com/sympy/sympy/pull/28115) is closed to being merged.

I finished writing tests and expanded the discrete functionality to MIMO systems.
Then, after some reviews, I made some minor changes to the code and we decided to rename `DTTransferFunction` to `DiscreteTransferFunction`.

I also opened two issues, which are closely related to PR [#28021(open)](https://github.com/sympy/sympy/pull/28021) I mentioned in a previous update and is ready to be merged:
- [#28176(Open)](https://github.com/sympy/sympy/issues/28176) - Simplify output of alternative Routh-Hurwitz test
- [#28180(Open)](https://github.com/sympy/sympy/issues/28180) - Performance issues in stability analysis with large symbolic matrices

I opened the first one thanks to a [comment](https://github.com/sympy/sympy/pull/28021#issuecomment-2985447168) by [@oscarbenjamin](https://github.com/oscarbenjamin). He found that there could be a significant simplification of the inequalities, because there are a lot of repeated factors and several terms are raised to even powers.

The second one is about some problems I encountered when studying the stability of a matrix with a large amout of symbols.
My PC wasn't able to compute them as it needed more memory.
I found that the characteristic polynomial calculation was too expensive because it tried to perform simplifications.
I found a possible solution using the `EXRAW` domain. More information could be found on github.
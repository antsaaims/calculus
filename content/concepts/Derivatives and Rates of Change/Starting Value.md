---
title: Starting Value
description: A rate-of-change graph tells you how F changes, but not F's actual value — you need one known starting point.
tags:
  - rate-of-change
  - graph-reading
---

Here's the catch with rate-of-change graphs: they only ever tell you about **change**,
never the actual value of $F$.

$$
F(x) = \underbrace{F(a)}_{\text{starting value (must be given)}} + \underbrace{\text{Change on }[a,x]}_{\text{signed area under } f}
$$

Without a known starting value $F(a)$, you can describe exactly how $F$ moves up and
down — but you can't pin down where it actually *is*.

**Math example:** if $f(x) = 2$ (constant) and $F(0) = 5$, then
$F(3) = 5 + \int_0^3 2\,dx = 5 + 6 = 11$.

**Real-world example:** two savings accounts can grow at the exact same rate all year
(same $f$) but hold very different balances at any moment, simply because they started
with different amounts $F(0)$.

**Further reading:** [The Fundamental Theorem of Calculus](https://math.libretexts.org/Bookshelves/Calculus/Calculus_(OpenStax)/05:_Integration/5.03:_The_Fundamental_Theorem_of_Calculus) (LibreTexts / OpenStax Calculus)

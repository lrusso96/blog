---
title:  Puzzle friendliness
description: The very basic definition of Puzzle friendliness.
categories: cryptography
tags: [Hash, Puzzle, Definition]
description: 
---

## Definition

Let us consider a hash function $H: \bits^* \to \bits^n$.

We say that $H$ is puzzle friendly if for every possible n-bit output value $y$, if $k$ is chosen from a distribution with high min-entropy, then it is infeasible to find $x$ such that $H(k \|\| x) = y$ in time significantly less than $2^n$.

---
title:  Search Puzzle
description: The very basic definition of Search Puzzle.
categories: cryptography
tags: [Bitcoin Core, Hash, Puzzle, Definition]
---

## Definition

A search puzzle consists of:

- a hash function $H$
- a value id, chosen from a high min-entropy distribution; we call this the puzzle identifier
- a target set $\mathcal{Y}$

A solution for the search puzzle is a value $x$ such that $H(id \| x) \in \mathcal{Y}$.

## Some considerations

Solving the puzzle requires finding an input so that the output falls within the set $\mathcal{Y}$, which is typically much smaller than the set of all outputs.
The size of the target set determines how hard the puzzle is.
If $\mathcal{Y}$ is the set of all $n$-bit strings, the puzzle is trivial, whereas if $\mathcal{Y}$ has only one element, the puzzle is maximally hard.

If a search puzzle is [puzzle-friendly]({% post_url 2020-08-08-puzzle-friendliness %}), this implies that there is no solving strategy for this puzzle which is much better than just trying random values of $x$.

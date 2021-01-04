---
title:  An NP-Complete Problem for Santa 🎅
description: An Algorithm Design exercise for Christmas.
categories: extra 
tags: [Exercise, NP]
article_header:
  type: overlay
  theme: dark
  background_color: '#203028'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(0, 0, 0 , .4), rgba(32, 0, 32, .4))'
    src: https://muskoka411.com/wp-content/uploads/2015/12/santa-claus.jpg

---

## The problem

Santa has a real challenge this year: 187 of his elves were quarantined with Covid-19 during this Christmas time, and are now clinically depressed because they missed all the fun.
He wants to give each of them a perfect present, and since they have always envied Santa for his magical sleigh, his idea is to give each of them his own toy sleigh.

Now in the shed, he has a set P of n pieces that will clearly e sufficient to build the sleighs, each of which is available in large amounts.
The pieces are such that you will never need more than a copy of any $p \in P$ for the same sleigh.

Santa, as an expert, knows what a good sleigh needs: for example they might each need a front light, and there might be different ones $(p_1, \dots, p_l)$ in P, so you must use $p_1$ or $\dots$ or $p_l$.
Santa has a long list of all kinds of different constraints on the sleigh assembly, which he is writing down similar as above.

As the new intern, Santa is calling you into his office and while you are eating a nice sugar cane, he tasks you with the following: tomorrow, it is your job to write and run a polynomial-time algorithm that gets as input a formal depiction of Santa's constraints, and outputs all 187 different sets of parts for the sleigh (if possible, otherwise return 'no').

Santa promises the assembly will be done by more experienced workers - all you have to take care of is that no two sleighs are exactly the same, so the gifts still feel special enough.
Despite the sugar cane, the assignment leaves a bitter taste in your mouth.
However, not wanting to ruin your own Christmas, you don't protest right away: that would look just lazy.
Come up with a mathematical proof that in general, this problem is clearly a hard one and might be not solvable for you in a day.

## Solution

I am going to show that the above problem is NP-complete.

### NP

First of all, note that given a solution, i.e. an assignment for $187 \cdot  \|P\|$ variables, we can check in polynomial-time its correctness: indeed, we simply verify that:

- each sleigh satisfies the constraints (clearly we assume the number of constraints is polynomial in $\|P\|$)
- each sleigh is unique (at most $186 + 185 + \dots + 1$ comparisons)

### NP-Hardness

We reduce the above problem to SAT.

Given an instance $s \in$ SAT expressed as a formula ($p_1$ or $p_2$ or $\dots$ or $p_k$) and $\dots$ and ($p_l$ or $\dots$ or $p_n$), we create an instance $t$ of the problem defined above as follows:

- we map each boolean variable $p_i$ to a component $p_i \in P$
- the formula of $s$ becomes the set of contraints for $t$
- we then create 187 *fake* components $y_i, i \in [1, 187]$
- finally, we add a *fake* sleigh contraint ($y_1$ or $y_2$ or $\dots$ or $y_{187}$)

At this point, we run the solving algorithm for $t$.

If we receive a "no" answer, we claim $s$ cannot be satisfied.
Otherwise, we take one of the sleighs (i.e. one of the different 187 assignments of $\|P\| + 187$ variables), we remove the fake $y_i$ variables from it and we return this as a solution for $s$.

### Does it work?

#### If $s$ is not satisfiable, $t$ is not satisfiable

This follows from the fact that Santa cannot find a single sleigh (and he should find 187 to solve the problem!) which satisfies the formula.
So, when Santa returns "no" for $t$, we can safely return "unsatisfiable" for $s$.

#### If $s$ is satisfiable, $t$ has at least one solution

Let $x$ be a valid assignment for $s$.
Then we claim $x'$ is a valid solution for $t$, where $x'$ is as follows:

- sleigh $i$ is exactly as $x$ and has $y_i = 1, y_j = 0, j \ne i$
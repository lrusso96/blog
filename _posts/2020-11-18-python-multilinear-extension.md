---
title: "[CTW11] - Multilinear Extension in Python"
description: An exercise by Justin Thaler
category: cryptography
tags: [Exercise, Python, Thaler, Zero-Knowledge]
article_header:
  type: overlay
  theme: dark
  background_image:
    gradient: 'linear-gradient(135deg, black, rgba(0, 0, 32, .7))'
---
## Overview

Here is an exercise proposed in the excellent manuscript **Proofs, Arguments, and Zero-Knowledge** by **Justin Thaler**.

See also [my solutions](https://github.com/lrusso96/proofs) on GitHub.

## The problem

Fix some prime p of your choosing. Write a Python program that takes as input
an array of length 2^l specifying all evaluations of a function f:{0,1} → Fp
and a vector r ∈ Fp and outputs f'(r).

## Solution

We are going to implement CTW11 algorithm in Python. This algorithm has O(n logn) running time and O(logn) space complexity.

### Warm-up

We first define a function `binaries` to produce all the possible binary strings of length n.

```python
def binaries(n):
    return list(map(list, product([0, 1], repeat=n)))
```

Then we define `prettify` function as:
```python
def prettify(l):
    return ",".join(map(str, l))
```

### Core

We initialize f'(r) = 0, and process each update (w,f(w)) via:
  - f'(r) ← f'(r) + f(w)·χw(r)

{% highlight python linenos %}
def CTW11(p: int, l: int, evaluations: List[int], r: List[int]) -> int:
    if 2**l != len(evaluations):
        print(f"You need to specify {2**l} values")
        exit(1)

    def chi(w: List[int], x: List[int]):
      ...

    ret = 0
    ctr = 0
    for w in binaries(l):
        ret += evaluations[ctr]*chi(w, r)
        ret = ret % p
        ctr += 1
    return ret
{% endhighlight %}

where `chi` is defined at line 6 as:
{% highlight python %}
def chi(w: List[int], x: List[int]):
    if len(w) != len(x):
        print(
            f"Cannot compute χw(x): w has length {len(w)} and x has length {len(x)}.")
        exit(1)
    pi = 1
    for i in range(len(r)):
        pi *= (x[i]*w[i] + (1 - x[i])*(1-w[i]))
        pi = pi % p
    return pi
{% endhighlight %}

## Run the code

To execute the snippet above, we can write a simple `main` program.

{% highlight python %}
if __name__ == "__main__":
    p = int(input("Insert a prime value p: "))
    l = int(input("Insert length l: "))
    evaluations = [int(input(f"f({prettify(i)}): ")) for i in binaries(l)]

    r = [int(input(f"r{i}: ")) for i in range(l)]

    output = CTW11(p, l, evaluations, r)
    print(f"The output f'({prettify(r)}) is: {output}")
{% endhighlight %}
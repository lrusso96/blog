---
title:  Impossibility of perfectly secret PKE
description: A simple proof to show that perfectly secret public-key encryption is impossible.
categories: cryptography
tags: [Encryption, Katz-Lindell, PKE, Exercise]
---

## Overview

Perfectly secret PKE is impossible, regardless of how long the keys are or how small the message space $\mathcal{M}$ is.
{:.success}

We sketch a proof by solving an exercise proposed by Katz and Lindell[^1].

## Exercise

Assume a public-key encryption scheme for single-bit messages with no decryption error.
Show that, given pk and a ciphertext $c$ computed via $c \samples \Enc_{pk}(m)$, an unbounded adversary can determine $m$ with probability 1. 

### Solution \#1

A possible approach could be brute-force to determine the secret key $sk$ associated with $pk$.
The attacker is unbounded, so he can run $\Gen(\cdot)$ many times until obtaining the right pair $(pk, sk)$.
Then, it can compute $m = \Dec(sk, c)$, and will succeed with probability 1.

### Solution \#2

An alternative approach could be brute-force $\Enc$ algorithm: the unbounded attacker will run $c' = \Enc(pk, \cdot, r)$ for all possible messages and for all possible randomness $r$, until $c = c'$.
Then, it knows the message $m$ (and even the randomness) and succeeds with probability 1.

[^1]: Exercise 11.1 - Katz, Lindell, Introduction to Modern Cryptography (II edition)
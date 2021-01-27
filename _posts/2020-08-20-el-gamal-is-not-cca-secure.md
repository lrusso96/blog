---
title:  El Gamal is not CCA-secure
description: A simple proof to show that El Gamal encryption scheme is not CCA-secure.
categories: cryptography
tags: [CCA, Encryption, Katz-Lindell, PKE, Exercise]
modify_date: 2021-01-27
---

## Overview
This is one of the exercises proposed by Katz and Lindell[^1].

## Solution
Given an El Gamal encryption scheme with publick key $pk = (\mathbb{G}, q, g, h=g^\alpha)$, the challenge ciphertext $c_b = (c_1, c_2)$, with $c_1 = g^r$ and $c_2 = h^r \cdot m_b$, the attacker can exploit the *malleability* in the following way: asks to decrypt $c = (c_1, c_2 \cdot k)$, for some message $k$ of its choice, and obtains a message $m$ from the oracle.
Then it easily retrieves $m_b = \frac{m}{k}$.

[^1]: Exercise 11.9 - Katz, Lindell, Introduction to Modern Cryptography (II edition)
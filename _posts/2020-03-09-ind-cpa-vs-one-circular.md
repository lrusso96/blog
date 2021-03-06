---
title:  IND-CPA Security and 1-Circular Security
description: A simple exercise.
categories: cryptography
tags: [CPA, Circular Security, Encryption, PKE, Exercise]
description: Show that IND-CPA Security does not imply 1-Circular Security.
---

## Overview
[IND-CPA Security]({% post_url 2020-03-09-ind-cpa-security %}) $\not\Rightarrow$ 1-[Circular Security]({% post_url 2020-03-09-circular-security %}).
{:.success}

## The short answer

It is quite easy to show that IND-CPA security does not
imply 1-circular security. Take any IND-CPA secure scheme $\Pi := ( \Gen, \Enc, \Dec)$ and construct a new scheme $\Pi' := (\Gen, \Enc', \Dec)$. On input the secret key $sk$, the encryption scheme $\Enc'$ outputs $sk$; otherwise computes $\Enc(\cdot)$ on the message.

The modified scheme is still IND-CPA, but its 1-circular security is completely broken.

### A few details

The algorithm $\Enc'$ takes in input only the public key $pk$, so how can it behave differently when it receives $sk$ as input? The trick here is to run $\Dec$, since it is a public algorithm as well, to check whether $m = sk$.

Indeed, compute $c \samples \Enc(pk, r)$, for a random message $r$ and then run $r' := \Dec(pk, sk:=m, c)$. If $r = r'$ we assume that $m$ is the secret key!

**Note:** To minimize the possibility of making a wrong assumption, we can run many times the protocol described above.

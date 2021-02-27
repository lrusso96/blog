---
title:  IND-RCCA Security
description: The basic definition of Indistinguishability under Replayable CCA.
categories: cryptography
tags: [RCCA, Encryption, PKE, Definition]
---

## Replayable CCA
### Definition

An encryption scheme $\Pi = (\Gen, \Enc, \Dec)$ is IND-RCCA-1 secure if for all PPT adversaries $A:=(A_1, A_2)$, $\Game_{\Pi, A}^{\textrm{RCCA}}( \lambda, 0) \approx_c \Game^{\textrm{RCCA}}_{\Pi, A}(\lambda, 1)$, where the game is the following:

$$\begin{aligned}
&&& \underline{\Game_{\Pi, A}^{\textrm{RCCA}}( \lambda, b)}: \\
& \\
&1. && (pk, sk) \samples \Gen(1^\lambda) \\
&2. && (m_0, m_1, z) \samples A_1^{\Dec(sk, \cdot)}(pk) \\
&3. && c \samples \Enc(pk, m_b) \\
&4. && b' \samples A_2^{\Dec^*(sk, \cdot)}(c, z)
\end{aligned}$$

The adversary has oracle access to $\Dec^*$, which returns a decryption $m$ of the input chipertext $c$; if $m \in \{m_0, m_1\}$, then the oracle returns a special symbol. This is the main difference with respect to the [CCA scenario]({% post_url 2020-03-21-ind-cca-security %}).

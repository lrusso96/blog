---
title:  IND-CPA Security
description: The very basic definition of Indistinguishability under CPA.
categories: cryptography
tags: [CPA, Encryption, PKE, Definition]
---

## Definition

An encryption scheme $\Pi = (\Gen, \Enc, \Dec)$ is IND-CPA secure if for all PPT adversaries $A:=(A_1, A_2)$, $\Game_{\Pi, A}^{\CPA}( \lambda, 0) \approx_c \Game^{\CPA}_{\Pi, A}(\lambda, 1)$, where the game is the following:

$$\begin{aligned}
&&& \underline{\Game_{\Pi, A}^{\CPA}( \lambda, b)}: \\
& \\
&1. && (pk, sk) \samples \Gen(1^\lambda) \\
&2. && (m_0, m_1, z) \samples A_1(pk) \\
&3. && c \samples \Enc(pk, m_b) \\
&4. && b' \samples A_2(c, z)
\end{aligned}$$

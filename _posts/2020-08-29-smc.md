---
layout: post
title: smc
date: 2020-08-29 00:00:00 +0100
description: A simple Rust crate for commitment schemes.
img: github.jpg
github_repo: smc
category: code
---
**smc** is a crate which provides a simple implementation of notable (academic) commitment schemes, on top of the popular OpenSSL cryptography library.

This is mostly an exercise to learn Rust. I took inspiration from the Secure Multiparty Computation class (@Sapienza Univerity of Rome).

## Supported commitment schemes

* El Gamal
* Pedersen

They can be used on top of groups where Discrete Logaritm problem is
assumed to be hard: currently, the crate supports both Multiplicative
Group Zp*, for a safe prime p, and Elliptic Curve.

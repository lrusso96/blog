---
title: "How to set-up Charm on Ubuntu"
description: Simple installation guide for Charm framework
category: cryptography
tags: [Python]
modify_date: 2021-03-23
article_header:
  type: overlay
  theme: dark
  background_image:
    gradient: "linear-gradient(135deg, black, rgba(0, 0, 32, .7))"
---

## What is Charm

[**Charm**](https://github.com/JHUISI/charm) is a Python framework for rapidly prototyping advanced cryptosystems.
It was designed from the ground up to minimize development time and code complexity.

Charm uses a hybrid design: performance-intensive mathematical operations are implemented in native C modules, while cryptosystems themselves are written in a readable, high-level language.
Charm additionally provides new components to facilitate the rapid development of new schemes and protocols.

## Installation

I have found the documentation a bit messy. For this reason, I have decided to write this simple post to explain how I have managed to install Charm v0.50 on my Ubuntu 20.4 machine.

### Requirements

As far as I know, Charm does not work with Python 3.8+ versions: the default branch is a _dev_ branch, and the latest stable release dates back to 2011!

The first thing to do is to set-up a Python 3.7.1 environment.
We start by downloading Python 3.7 binaries.

```
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.7 python3.7-dev
```

Then we can install _virtualenv_ to manage the virtual environment; we name this environment _py37_ and, finally, we activate it.

```
sudo apt install virtualenv
virtualenv -p /usr/bin/python3.7 py37
source py37/bin/activate
```

### Dependencies

Charm relies on some libraries. So we can install them by running

```
sudo apt-get install -y libgmp10 libgmp-dev
sudo apt-get install -y openssl
```

At this point, we can clone the Charm GitHub repository and install all the other dependencies

```
git clone https://github.com/JHUISI/charm
cd charm
pip install -r requirements.txt
```

### Build

We try to build Charm running the following commands

```
./configure.sh
cd ./deps/pbc && make && sudo ldconfig && cd -
make
make install && sudo ldconfig
```

### Test

To assess that the installation is successful, we can run the test suite

```
make test
```

## Have fun with Charm!

Once the installation finishes and the test suite passes (despite some warnings), we are ready to prototype cryptographic systems from scratch or on top of already-implemented schemes: take a look at the [official documentation](https://jhuisi.github.io/charm/).

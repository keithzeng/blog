---
title: "Probability"
date: 2019-01-24T22:27:30-08:00
categories: ["mathematic"]
series: ["statistical learning"]
tags: ["probability", "CSE250B", "notes"]
draft: false
---
# Discrete Random Variables #
A *random variable* is a number whose value depends upon the outcome of a random experiement. Such as tossing a coin 10 times and let *X* be the number of Head.

A *discrete random variable* **X** has finitely countable values $x_i = 1, 2...$ and $p(x_i) = P(X = x_i)$ is called *probability mass function*.

Probability mass functions has following properties:

1. For all i, $p(x_i) > 0$
1. For any interval $P(X \in B) = \sum_{x_i \in B}p(x_i)$
1. $\sum_{i}p(x_i) = 1$

There are many types of discrete random variable

1. Unifrom discrete random variable
  - $\mathbb{E} = \frac{x_1 + x2+ ...}{n}$
1. Bernoulli Random Variable
  - $\mathbb{E} = p$
1. Binomial random variable
  - $\mathbb{E} = np$
  - Probability mass function $P(X = i) = C(n, i)p^i(1-p)^{n - i}$
1. Poisson random variable
  - $P(x = i) = \frac{\lambda^i}{i!}e^{-\lambda}$
  - $\mathbb{E} = \lambda$
1. Gemometric random variable
  - $P(X = n) = p(1 - p)^{n - 1}, where n = 1, 2, ...$
  - $\mathbb{E} = \frac{1}{p}$

# Coninuous Random Variables #
A random variable X is continuous if there exists a nonnegative function f so that, for every interval B,
$$
P(X \in B) = \int_{B}f(x)dx
$$

and f(x) is called the density of X.
Also, it must hold that$\int_{-\infty}^{\infty}f(x)dx = 1$.

The function F = F(X) given by
$$
F(x) = P(X <= x) = \int_{-\infty}^{x}f(s)ds
$$

is called the distribution function of X and $F'(x) = f(x)$.

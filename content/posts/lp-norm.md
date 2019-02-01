---
title: "lp norm"
date: 2019-01-31T17:02:35-08:00
categories: ["machine learning"]
series: ["statistical learning"]
tags: ["lpnorm", "notes"]
draft: false
---

## Families of Distance Function

### $l_p$ norm

The most common one is $l_2$ norm (Euclidean distance):

$$||x - z||_2 = \sqrt{\sum\_{i=1}^{m}(x_i - z_i)^2}$$

*Notes: sometime 2 is dropped.*

For $p \geq 1$, the $l_p$ distance:

$$||x - z||_p = (\sum\_{i=1}^{m}(x_i - z_i)^p)^{1/p}$$

Special case:

$l_1$ distance:
$$||x - z||_1 = \sum\_{i=1}^{m}|x_i - z_i|$$

$l_\infty$ distance:

$$||x - z||_1 = max_i |x_i - z_i|$$

### Metric space

Let $X$ be the space that data lie.

A distance function  d: $X$ x $X$ -> $\mathbb{R}$ is metric if:

- $d(x, y) \geq 0$ (nonnegativity)
- $d(x, y) = 0 iff x = y$
- $d(x, y) = d(y, x)$ (symetry)
- $d(x, z) \leq d(x,y) + d(y, z)$ (triangle inequality)

### Non-metric Function
Let p, q be the probability distributions on some $X$.

The **Kullback-Leibler divergence** or **relative entropy** between p, q is:

$$d(p,q) = \sum_{x\in X} p(x) log \frac{p(x)}{q(x)}$$
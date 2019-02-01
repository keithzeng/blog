---
title: "Marginal Distribution"
date: 2019-01-31T17:57:34-08:00
categories: ["mathematic"]
series: ["probability"]
tags: ["distribution"]
draft: false
---

## Marginal Distribution:

It's a function that gives the probability based on only subset of the variables.[^marginal]. For example,

![Joint Distribution](/img/cse250/joint-distribution.png)

Or in mathematical way, for discrete

$$Pr(X = x) = \sum_y Pr(X = x, Y = y) = \sum_y Pr(X = x | Y = y) Pr(Y = y)$$

and for continuous

$$p_X(x) = \int_y p\_{X,Y}(x,y) dy = \int_y p\_{X|Y}(x|y)p_Y(y) dy$$

and it can also be written as Expected Vaue

$$p\_X(x) = \int\_y p\_{X|Y} (x|y) p\_Y(y) dy = \mathbb{E}\_Y[p\_{X|Y} (x|y)]$$

[^marginal]: Mariginal Distribution, https://en.wikipedia.org/wiki/Marginal_distribution
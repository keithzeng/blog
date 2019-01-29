---
title: "Merge Sort"
date: 2019-01-29T01:14:32-08:00
categories: ["algorithm"]
series: ["divide and conquer"]
tags: ["CSE202", "notes"]
draft: false
---

## Problem ##
Sort the elements

Abstract the behavior:\
1. Divide the input into two pieces of equal size O(n)
1. solve the two subproblems on these pieces separately by recursion
1. combine the two results into an overall solution O(n)

## Recurrence ##

Time Complexity:

T(n) ≤ 2T(n/2) + cn

To analyze the above recurrence relation, check below image.
![Recurrence](/img/cse202/recurrence-tree.png)

- At level j, we have $2^j$ nodes with size $n/2^j$
- Each node takes $cn/2^j$, so level j takes $cn/2^j$ x $2^j = cn$
- There are logn levels, so T(n) = O(nlogn)

For more general case

T(n) ≤ qT(n/2) + cn

Check below:
![Recurrence](/img/cse202/recurrence-tree-q.png)

- At level j, we have $q^j$ nodes with size $n/2^j$
- Each node takes $cn/2^j$, so level j takes $cn/2^j$ x $q^j = (q/2)^jcn$
- So
$$T(n) \leq cn\sum_{j=0}^{\log_2 {n-1}}(\frac{q}{2})^j$$

Since this is a geometric series with r = q/2
$$T(n) \leq cn\frac{r^{\log_2 n} - 1}{r - 1} \leq cn\frac{r^{\log_2 n}}{r - 1}$$

We then move the r - 1 out to form the constant
$$T(n) \leq \frac{c}{r - 1}nr^{\log_2 n}$$

To figure out what is $r^{\log_2 n}$, we use $a^{\log b} = b^{\log a}$ when a > 1 and b > 1.

So, $r^{log_2 n} = n^{\log_2 r} = n^{\log_2 \frac{q}{2}} = n^{{\log_2 q} - 1}$

Thus, we have
$$T(n) \leq \frac{c}{r - 1}nn^{\log_2 q - 1} \leq \frac{c}{r - 1}n^{\log_2 q} = O(n^{\log_2 q})$$

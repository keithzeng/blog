---
title: "Sequence Alignment"
date: 2019-02-09T17:56:45-08:00
categories: ["algorithm"]
series: ["dynamic programing"]
tags: ["dp"]
draft: false
---

## Problem[^algo]

When you type "ocurrance", the brower will will prompt “Perhaps you mean occurrence?”

How does the search engine knows?

How does it know the most similar word?

How do we determine the similarity between words?

The definition of similarity will be based on the optimal alignment between X and Y where  X = $x_1x_2 . . . x_m$, Y = $y_1y_2 . . . y_n$.

1. when there is gap (character not matched), we pay $\delta$
1. when we match character p and q, we pay $\alpha\_{pq}$, where $\alpha\_{pq}$ = 0
1. goal is to minimize the sum of cost.

In the optimal alignment

1. (m,n) $\subset$ M
1. the $m^{th}$ position of X is not matched
1. the $n^{th}$ position of Y is not matched

Then we have following

1. OPT(m, n) = $\alpha_{x_my_n}$ +OPT(m−1,n−1)
1. OPT(m,n)= $\delta$ + OPT(m−1,n)
1. OPT(m, n) = $\delta$ + OPT(m, n − 1).

Therefore we have

$$OPT(i,j)=\min[\alpha\_{x_iy_j} +OPT(i−1,j−1),\delta + OPT(i−1,j),\delta+OPT(i,j−1)]$$

## Algorithm
Alignment(X ,Y )

- Array A[0...m,0...n]
- Initialize A[i, 0]= i$\delta$ for each i
- Initialize A[0,j]=j$\delta$ for each j
- For j=1,...,n
  - For i=1,...,m
     - Use the recurrence (6.16) to compute A[i, j]
  - Endfor
- Endfor
- Return A[m, n]


## Analysis

Running time = O(mn). Space = O(mn)

[^algo]: Algorithm Design by Jon Kleinber, Eva Tardos 
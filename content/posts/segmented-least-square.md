---
title: "Segmented Least Square"
date: 2019-02-09T12:54:29-08:00
categories: ["algorithm"]
series: ["dynamic programing"]
tags: ["dp"]
draft: false
---

## Problem[^algo]

Data $P = (x_1,y_1), (x_2, y_2)...(x_n, y_n)$ for $x_1 < x_2 < ... < x_n$.

Given a line y=ax+b, and error

$$Error(L, P) = \sum\_{i=1}^n(y_i - ax_i -b)^2$$

![line_mse](/img/cse202/line_mse.png)

And it has closed form solution of 

$$a = \frac{n\sum_i x_iy_i - (\sum_i x_i)(\sum_i y_i)}{n\sum_i x_i^2 - (\sum_i x_i)^2}$$

and

$$b = \frac {\sum_i y_i - a \sum_i x_i}{n}$$

However, if the data is show as below (maybe fitted with two lines), we can't just use the above formula.

![line_two](/img/cse202/line_two.png)

**Formulated Problem**

- $P = \{p_i | i = 1\ to\ n\}$, where $p_i = (x_1, y_1)$, with x1 < x2 < . . . < xn
- observing that $p_n$ belongs to a segment, and that segment start at some index i
- then we can recursively look for $p_1 ..., p\_{i-1}$.
- OPT(i) = Optimal solution for $p_i, ..., p_i$.
- $OPT(n) = e\_{i,n} + C + OPT(i − 1)$
- $OPT(j) = \min\_{1≤i≤j} (e\_{i,j} + C + OPT(i − 1))$ (6.7)

## Algorithm

Segmented-Least-Squares(n)

- Array M[0...n]
- Set M[0]=0
- For all pairs i≤j
  - Compute the least squares error $e\_{i , j}$ for the segment $p_i , . . . , p_j$
- EndFor
- For j=1,2,...,n
  - Use the recurrence (6.7) to compute M[j]
- Endfor
- Return M[n]

![line_graph](/img/cse202/line_graph.png)

## Analysis

Perform error, $e\_{i,j}$, calculation for all pair of i and j takes O($n^2$) to loop and O(n) based on formula, so overall O($n^3$) times.

To get OPT takes O($n^2$).

[^algo]: Algorithm Design by Jon Kleinber, Eva Tardos 
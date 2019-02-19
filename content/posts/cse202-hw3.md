---
title: "CSE202 HW3"
date: 2019-02-18T19:32:41-08:00
categories: ["algorithm"]
series: ["dynamic programing"]
tags: ["cse202",dp"]
draft: true
---
## Problem 1
### Algorithm

### Analysis

## Problem 2 (KT 6.11)

### Idea
Let OPT[i] denote the minimum cost for cost up to week i. For each week i, we have choice of either using A or B. So the OPT[i] reduces to following:

$$ OPT[i] = 
\begin{cases}
OPT[i - 1] + r * s_i \newline
OPT[i - 4] + 4 * c \newline
\end{cases}
$$

which is then reduces to follwoing

$$OPT[i] = \min(OPT[i - 1] + r * s_i , OPT[i - 4] + 4 * c)$$

### Algorithm

ALGO(n, s, c):

Let OPT = array of 0's with size n + 1\
Let OPT[0] = 0

for i = 1 to n

  - if i < 4: OPT[i] = OPT[i - 1] + r * s_i
  - else OPT[i] = min(OPT[i - 1] + r * s_i , OPT[i - 4] + 4 * c)

return OPT[n]

### Analysis

#### Space Complexity

OPT takes O(n).

#### Time Complexity

We only have 1 loop which iterates up to n, so O(n).

## Problem 3 (KT 7.5)

False. The (A,B) is no longer the minimum cut. Consider the following example.

![cut-counterexample](/img/cse202/cut-counterexample-before.png)

![cut-counterexample](/img/cse202/cut-counterexample-after.png)

Initially $A^\*$ = {s, u} with c(A,B) = 3, if we increase the weight by 1 to every edge the new $A^\*$ = {s} with c(A,B) = 5.

## Problem 4
### Algorithm

### Analysis
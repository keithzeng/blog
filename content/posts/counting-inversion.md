---
title: "Counting Inversion"
date: 2019-01-29T22:37:45-08:00
categories: ["algorithm"]
series: ["divide and conquer"]
tags: ["cse202","notes"]
draft: false
---

## Problem

Application in ranking, also called corraborative filtering.

Comparing two rankings and decide how similar they are, 
or how many pairs are out of order.

To quantify this, we count the number of inversions. The inversion is defined as two indices i < j that $a_i > a_j$.
![Inversion Example](/img/cse202/inversion.png)

## Algorithm

### Brute-Force
$T(n) = O(n^2)$

### Modified Merge-Sort

By leverage the merge process form merger-sort, we can count the number of inversion.
![merge and count](/img/cse202/merge-and-count.png)

Basically, when the element from A is appended, there is not inversion. When we append element from B, the reamining number in the A is the number of inversion.

#### Merge and Count
![inversion-merge-count-algorithm](/img/cse202/inversion-merge-count-algorithm.png)

#### Sort and Count
![inversion-sort-count-algorithm](/img/cse202/inversion-sort-count-algorithm.png)

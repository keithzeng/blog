---
title: "Sequence Alignment Revisited"
date: 2019-02-09T18:50:42-08:00
categories: ["algorithm"]
series: ["dynamic programing"]
tags: ["dp", "divide and conquer"]
draft: false
---

## Problem[^algo]

[Sequence Alignment](../sequence-alignment)

We can reduce the space by using only two column instead.


Space-Efficient-Alignment(X ,Y)

- Array B[0...m,0...1]
- Initialize B[i,0]=iδ for each i (just as in column 0 of A)
- For j=1,...,n
  - B[0,1]=j$\delta$ (since this corresponds to entry A[0,j])
  - For i=1,...,m
     - B[i, 1]= min[$\alpha x_iy_j$ + B[i − 1, 0], $\delta$ + B[i−1,1], $\delta$ + B[i,0]]
  - Endfor
  - Move column 1 of B to column 0 to make room for next iteration:
     - Update B[i, 0]= B[i, 1] for each i
- Endfor

However, this doesn't left enough information to get back the information about alignment.

In the previous problem, we can define f(i, j) to be shortest path from (0,0) to (i, j), we define g(i, j) to be the shortest path from (i,j) to (m,n).

Analogously, we have

$$g(i,j)=\min[\alpha_{x\_{i+1}y\_{j+1}} +g(i+1,j+1),\delta + g(i,j+1),\delta+g(i+1,j)]$$

Therefore, the length of the shortest corner-to-corner path in $G\_{XY}$ that passes through (i, j) is f(i, j) + g(i, j).

## Claim
Let k be any number in {0,...,n}, and let q be an index that minimizes the quantity f (q, k) + g(q, k). Then there is a corner-to-corner path of minimum length that passes through the node (q, k).

## Proof

For k $\in$ {0, n}, the shortest path must go through some node p in kth column.
$$l^* = f(p,k) + g(p,k)$$

Also assume that q in the node minize in this column
$$f(p,k) + g(p,k) \geq l^* = f(q,k) + g(q,k)$$

So we have
$$l^* \geq f(q,k) + g(q,k)$$

But since $l^\*$ is the minimum, we also have

$$l^* \leq f(q,k) + g(q,k)$$

Therefore, we have

$$l^* = f(q,k) + g(q,k)$$

Then this path can use at most O(m + n) space.

## Algorithm

Divide-and-Conquer-Alignment(X ,Y )

- Let m be the number of symbols in X
- Let n be the number of symbols in Y
- If m≤2 or n≤2 then
  - Compute optimal alignment using Alignment(X,Y)
- Call Space-Efficient-Alignment(X,Y[1:n/2])
- Call Backward-Space-Efficient-Alignment(X,Y[n/2+1:n])
- Let q be the index minimizing f(q,n/2)+g(q,n/2)
- Add (q, n/2) to global list P
- Divide-and-Conquer-Alignment(X[1 : q],Y[1 : n/2])
- Divide-and-Conquer-Alignment(X[q + 1 : n],Y[n/2 + 1 : n])
- Return P

## Analysis

Space is clearly O(m+n).

Running time is

\begin{align}
T(m, n) &\leq cmn + T(q, n/2) + T(m − q, n/2) \newline
T(m,2) &\leq cm \newline
T(2, n) &\leq  cn
\end{align}

Assuming m = n, we got

\begin{align}
T(n) &\leq 2T(n/2) + cn2 \newline
T(n) &= O(n^2)
\end{align}

Back to original problem, now assume that T(m, n) = kmn

\begin{align}
T(m, n) &\leq cmn + T(q, n/2) + T(m − q, n/2) \newline
&\leq  cmn + kqn/2 + k(m − q)n/2 \newline
&= cmn + kqn/2 + kmn/2 − kqn/2 \newline
&= (c + k/2)mn
\end{align}

So we can infer that k = 2c should work.

[^algo]: Algorithm Design by Jon Kleinber, Eva Tardos 
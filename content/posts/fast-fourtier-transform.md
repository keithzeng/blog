---
title: "Fast Fourtier Transform"
date: 2019-01-30T00:31:46-08:00
categories: ["algorithm"]
series: ["divide and conquer"]
tags: ["cse202", "notes"]
draft: false
---

## Problem

Given two vectors $a = (a_1, a_2, a\_{n-1})$ and $b = (a_1, b_2, b\_{n-1})$.

The convolution of a * b is a vector with 2n - 1 coordinates, where coordinate k is $\sum_{(i,j):i+j=k|i,j < n} a_ib_j$, which is can be written as

$$a ∗ b = (a_0b_0, a_0b_1 + a_1b_0, a_0b_2 + a_1b_1 + a_2b_0, . . . ,
a\_{n−2}b\_{n−1} + a\_{n−1}b\_{n−2}, a\_{n−1}b\_{n−1})$$

Or an n x n table, whose (i, j) entry is $a_ib_j$

\begin{bmatrix}
a_0b_0 & a_0b_1 & ... & a_0b\_{n-2} & a_0b\_{n-1}\newline
a_1b_0 & a_1b_1 & ... & a_2b\_{n-2} & a_1b\_{n-1}\newline
a_2b_0 & a_2b_1 & ... & a_2b\_{n-2} & a_2b\_{n-1}\newline
... & ... & ... & ... & ... \newline
a\_{n-1}b_0 & a\_{n-1}b_1 & ... & a\_{n-1}b\_{n-2} & a\_{n-1}b\_{n-1}
\end{bmatrix}

Then the convolution is suming along the diagonols. The motivation for convultion lies on the polynomial applications, signaling.

**Extra notes**

For example, we have a vector representing the measurement. We would like to smooth out the noise for each measurement $a_i$ with weighted sum of its left neighbors and right neighbors within k steps.

## Algorithm

### Preprocess:

1. Choose 2n values $x_1, x_2, ..., x\_{2n}$, evaluate $A(x_j)$ and $B(x_j)$ for j=1 ... 2n
1. $C(x_j) = A(x_j)B(x_j)$
1. Reconstruct $C(x_j)$ from its values on $x_1, x_2, ..., x\_{2n}$

### The Complex Roots of Unity
[Complex Number](https://www.math.toronto.edu/mathnet/questionCorner/epii.html)
![Complex Number](/img/cse202/complex-number.png)
A complex number can be represented in rectangular form as $z = x + iy$.\
Or $z = r(cos\theta + isin\theta)$\
Or in polar coordinate $z = re^{\theta i}$

Combine these, we get $e^{i\theta} = cos\theta + sin\theta$
Plug in $\theta = \pi$, we got $e^{i\pi} = -1$, which leads to the Euler's identity $e^{i\pi} + 1 = 0$.

For each polynomial equation $x^k = 1$, the complex roots $\omega\_{j,k} = e^{2\pi ji/k}$, since $(e^{2\pi ji/k})^k = e^{2\pi ji} = (e^{2\pi i})^j = 1 ^ j = 1$. We refer $\omega$ as the *kth root of unity*.

For k = 8, we got following
![8th-root-of-unity](/img/cse202/8th-root-of-unity.png)

Step 1.
Going back to the evaluating A(x), let's split A(x) into
$$A\_{even}(x) = a_0 + a_2x + a_4x^2 + ... + a\_{n−2}x^{(n−2)/2}$$
and
$$A\_{odd}(x) = a_1 + a_3x + a_5x^2 + ... + a\_{n−1}x^{(n−2)/2}$$\
And $A(x) = A\_{even}(x^2) + xA\_{odd}(x^2)$

Step 2.
Now considering we got the 2nth root of unity, $\omega\_{j,2n} = e^{2\pi ji/2n}$, we can simply obtain the nth root by squaring the 2nth root, $\omega\_{j,k}^2 = e^{2\pi ji/n}$. This only takes constant operation, so we got
$$A(\omega\_{j, 2n}) = A\_{even}(\omega\_{j, 2n}^2) + \omega\_{j, 2n}A\_{odd}(\omega\_{j, 2n}^2)$$

Step 3.
For $C(\omega\_{j,n}) = A(\omega\_{j,2n})B(\omega\_{j,2n})$, it takes O(n) times. Reconstruction takes similar approach as before. Let's define C(x) $C(x) = \sum_{s=0}^{2n-1} c_sx^s$, which we want to reconstruct from its values $C(\omega\_{s,2n})$ at 2nth root of unity. Let's define another $D(x) = \sum\_{s=0}^{2n-1} d_sx^s$ where $d_s = C(\omega\_{s,2n})$. Then,

\begin{align}
D(\omega\_{j,2n}) &= \sum_{s=0}^{2n - 1}C(\omega\_{s,2n})\omega\_{j,2n}^s \newline
&= \sum\_{s=0}^{2n - 1} (\sum\_{t=0}^{2n - 1} c_t\omega\_{s,2n}^t)\omega\_{j,2n}^s \newline
&= \sum\_{t=0}^{2n - 1} c_t(\sum\_{s=0}^{2n - 1} \omega\_{s,2n}^t\omega\_{j,2n}^s)
\end{align}

Using the fact that $\omega\_{s,2n} = (e^{2pii/2n})^s$, the above expression
\begin{align}
D(\omega\_{j,2n}) &= \sum\_{t=0}^{2n - 1} c_t(\sum\_{s=0}^{2n - 1} e^{(2\pi i)(st+js)/2n}) \newline
&= \sum\_{t=0}^{2n - 1} c_t(\sum\_{s=0}^{2n - 1} \omega\_{t+j,2n}^s)
\end{align}



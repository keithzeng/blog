---
title: "Positive Semi Definite"
date: 2019-02-07T15:29:45-08:00
categories: ["mathematic"]
series: ["matrix"]
tags: ["psd"]
draft: false
---

## PSD

[differential equation](https://www.comp.nus.edu.sg/~cs5240/lecture/matrix-differentiation.pdf)

Any matrix $A\_{d \times d}$ is said to be PSD if $x^TAx \geq$ 0 $\forall$ vector $x\_{d \times 1}$.

## Examples

### Identity matrix $I\_{d \times d}$:

$$
A = 
\begin{bmatrix}
1 & 0 & 0 & 0 \newline
0 & 1 & 0 & 0 \newline
0 & 0 & 1 & 0 \newline
0 & 0 & 0 & 1
\end{bmatrix}
$$

Then 

\begin{align}
x^TAx &= \sum\_{i = 1}^d \sum\_{i = 1}^d A\_{i,j}x_ix_j \newline
&= \sum\_{i = 1}^d A\_{i,i} x_i^2\newline
&= \sum\_{i = 1}^d x_i^2 \newline
&\geq 0
\end{align}

### Simple Matrix

$$
A = 
\begin{bmatrix}
2 & -1 \newline
-1 & 1 \newline
\end{bmatrix}
$$

\begin{align}
x^TAX &=
\begin{bmatrix}x_1 & x_2\end{bmatrix}
\begin{bmatrix}2 & -1 \newline -1 & 1\end{bmatrix}
\begin{bmatrix}x_1 \newline x_2\end{bmatrix}\newline
&= 2x_1^2 + x_2^2 - 2x_1x_2 \newline
&= (x_1-x_2)^2 + x_1^2 \newline
&\geq 0
\end{align}

### Diagonal Matrix

$$
A = 
\begin{bmatrix}
A\_{11} & ... & 0 \newline
0 & A\_{22} & ... \newline
... & ... & ... \newline
0 & 0 & A\_{dd}
\end{bmatrix}
$$

$$x^TAX = \sum\_{i=1}^d A\_{ii}x_i^2$$

If we conisder vector x to be
\begin{bmatrix}
1 \newline
0 \newline
... \newline
0 \newline
\end{bmatrix}

$A\_{11}$ has to be $\geq$ 0, same logic applies to other A's.

So if All $A\_{ii} \geq$ 0, then A is PSD.

## Properties of PSD

1. For any matrix A that is PSD, cA is also PSD, if c $\geq$ 0.
1. Given two PSD matrices, A and B, (A + B) is also PSD
  - Proof: $x^T(A + B)X = x^TAx + x^TBX \geq 0 \forall x \subseteq R^d$
1. A matrix M is PSD iff M can be written as $M = UU^T$ for some matrix U.
  - Proof: $UU^T$ is square
  - $x^TMx = x^TUU^Tx = (U^Tx)^T U^Tx = ||U^Tx||^2 \geq 0$

## Convexity
1. convexity: a function f: R $\rightarrow$ R is convex iff its second derivative $\geq$ 0 everywhere
1. A function f: R $\rightarrow$ R is convex iff its Hessian is PSD

### Examples

**Example 1**

Let $x \in R^d$$

$$f(x) = ||x||^2 = x^T x$$

$$\nabla f = 2x$$

$$\nabla^2 f = 2I$$

$\therefore$ it is PSD, since c $\geq$ 0 and I is PSD.

**Example 2**

Let $x = M\_{1 \times d}$ and $u = M\_{d \times 1}$

$$f(x) = (ux)^2$$

$$\nabla f = 2uxu$$

$$\nabla^2 f = 2uu^T$$

Since $uu^T$ is PSD, $2uu^T$ is also PSD.

**Example 3**

\begin{align}
L(w) &= \sum\_{i=1}^n (y^{(i)} - (w \cdot x^{(i)}))^2 \newline
&= (y - xw)^T(y - xw) \newline
&= y^Ty - 2y^Txw + w^Tx^Txw
\end{align}

Then

$$\nabla f = 2y^Tx + 2w^Tx^Tx$ using $\frac {dx^TAx}{dx} = x^T(A + A^T)$$

$$\nabla^2 f = 2x^Tx$$

Since $x^Tx$ is PSD, $2x^Tx$ is also PSD.

**Example 4**

$$L(w) = \sum\_{i=1}^n \ln (1 + e^{-y^{(i)} w \cdot x^{(i)}})$$

\begin{align}
\frac {\partial L(w)} {\partial w_j} &= \sum\_{i=1}^n \frac{e^{-y^{(i)} w \cdot x^{(i)}}(-y^{(i)}x_j^{(i)})}{1 + e^{-y^{(i)} w \cdot x^{(i)}}} \newline
&= \sum\_{i=1}^n \frac{-y^{(i)}x_j^{(i)}}{1 + e^{y^{(i)} w \cdot x^{(i)}}}
\end{align}


\begin{align}
\frac {\partial L(w)} {\partial w_j w_k} &= \sum\_{i=1}^n \frac{e^{y^{(i)} w \cdot x^{(i)}}y^{(i)}x_j^{(i)}y^{(i)}x_k^{(i)}}{(1 + e^{y^{(i)} w \cdot x^{(i)}})^2} \newline
&= \sum\_{i=1}^n \frac{e^{y^{(i)} w \cdot x^{(i)}}y^{(i)2} x_j^{(i)}x_k^{(i)}}{(1 + e^{y^{(i)} w \cdot x^{(i)}})^2} \newline
\end{align}

So Hessian

$$H = \sum\_{i=1}^n \frac{e^{y^{(i)} w \cdot x^{(i)}}y^{(i)2}(x^{(i)})^T(x^{(i)})}{(1 + e^{y^{(i)} w \cdot x^{(i)}})^2}$$

$\therefore$ H is PSD.


**Example 5**

Let $u = M\_{d \times 1}$

$$f(x) = e^{u \cdot w}$$

$$\nabla f = e^{u \cdot w}u$$

$$\nabla^2 f = e^{u \cdot w}u^Tu$$

Since $u^Tu$ is PSD, H is PSD.


**Example 6**

$$L(x) = \sum\_{i=1}^n (y^{(i)} - (w \cdot x^{(i)}))^2 + \lambda ||w||^2$$

$$\frac{\partial L}{\partial w_j} = -2 \sum\_{i=1}^n (y^{(i)} - (w \cdot x^{(i)}))x_j^{(i)} + 2 \lambda w_j$$

$$\frac{\partial L}{\partial w_j \partial w_k} =
\begin{cases}
2 \sum\_{i=1}^n x_j^{(i)2} + 2\lambda \text{, if k = j}  \newline
2 \sum\_{i=1}^n x_j^{(i)}x_k^{(i)} \text{, if k != j}
\end{cases}
$$

$$H = 2 x^Tx + 2\lambda I$$

$\therefore$ H is PSD.



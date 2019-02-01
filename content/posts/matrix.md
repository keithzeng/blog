---
title: "Matrix"
date: 2019-02-01T02:06:44-08:00
categories: ["mathematic"]
series: ["matrix"]
tags: ["determinant", "rank"]
draft: false
---

# Determinant

## Calculation
Determinant of 2x2 matrix

$$
A=
\begin{bmatrix}
a & b \newline
c & d
\end{bmatrix}
$$

$|A| = det(A) = ad -bc$

Determinant of 3x3 matrix, also called expansion of the determinant by first row. [Link](https://math.oregonstate.edu/home/programs/undergrad/CalculusQuestStudyGuides/vcalc/deter/deter.html).

$$
B=
\begin{bmatrix}
a & b & c \newline
d & e & f \newline
g & h & k
\end{bmatrix}
$$

$|B| = det(B) = 
a\begin{vmatrix}
e & f \newline
h & k
\end{vmatrix}
-b\begin{vmatrix}
d & f \newline
g & k
\end{vmatrix}
+c\begin{vmatrix}
d & e \newline
g & h
\end{vmatrix}$

Or we can replicate first two columns, we got
$$
\begin{bmatrix}
a & b & c & a & b\newline
d & e & f & d & e\newline
g & h & k & g & h
\end{bmatrix}
$$

$|B| = (aek + bfg + cdh) - (bdk+afh+ceg)$, which is adding the sum of products of diagonals from top left to bottom right minus sum of products of diagonals from top right to bottom left.

## Singular (degenerate) Matrix

if det(A) = 0, we call A is singular.

# Rank

The rank of a matrix A is the dimension of the space generated (or spanned) by its columns, which is maximal number of linearly independent columns of A (or rows). Rank is thus a measure of the "nondegenerateness" of the system of linear equations.


### Full rank
If matrix's rank = min(rows, columns)

### Rank Deficient:
If matrix is not full rank.

### For example:

\begin{bmatrix}
1 & 0 & 1 \newline
-2 & -3 & 1 \newline
3 & 3 & 0
\end{bmatrix}

Rank = 2, since the last column 2 = column 0 - columm 1

$$
A =
\begin{bmatrix}
1 & 1 & 0 & 2 \newline
-1 & -1 & 0 &-2
\end{bmatrix}
$$

Rank(A) = 1

$$A^T=
\begin{bmatrix}
1 & -1 \newline
1 & -1 \newline
0 & 0 \newline
2 & -2
\end{bmatrix}
$$

$Rank(A^T) = 1$, $Rank(A) = Rank(A^T)$, 


[^wiki]: rank, https://en.wikipedia.org/wiki/Rank_(linear_algebra)

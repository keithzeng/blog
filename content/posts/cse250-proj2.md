---
title: "CSE250 Proj2"
date: 2019-02-18T10:37:54-08:00
categories: ["machine learning"]
series: ["statistical learning"]
tags: ["cse250b", "project", "coordinate descent"]
draft: true
---

## Coordinate Descent
(a) In this project I used cyclic coordinate descent method(CCD), where I update each coordinate in order. Since the loss function is unconstrained, the function needs to be convex, smooth and Lipschitz continuously differentiable.[^revival] I also compare this method to another popular method random coordinate descent method(RCD).

(b) 
For every iteration, the coordinate, i, being picked will be updated with the value that minimize the loss function while fixing other $w_j \forall j \neq i$. 



**Pseudocode**

CCD()

1. Initialize w = array of 0's
1. Let k = number of features
1. Until converged or max iterations reach
  - for i = 1 to k
     - $w_i$ = value minimizes loss function while fixed other $w_j$

RCD()

1. Initialize w = array of 0's
1. Let k = number of features
1. Until converged or max iterations reach
  - i = choose i random from range of k
  - $w_i$ = value minimizes loss function while fixed other $w_j$

## Convergence

In order to converge, as stated above, the cost function needs to be smooth and convex. It is also been proved by Luo and Tseng that if these requirements are satisfied, the coordinate descent method will converge asymptotically.[^luotseng]

## Experimental Results

I used sklearn LogisticRegression model to compute the coefficient and the loss function.

The coefficient w is

\begin{bmatrix}
-16.7450 \newline
15.6933 \newline
52.4835 \newline
-6.9896 \newline
-0.1750 \newline
-11.4890 \newline
28.1081 \newline
-8.4948 \newline
-7.3612 \newline
7.7372 \newline
-49.5212 \newline
-3.8878 \newline
0.2811 
\end{bmatrix}

The loss $L^\*$ = 0.0182.

By running the CCD RCD methods, I got following graph

![compare](/img/cse250/proj2_compare.png)

As one can see, the CCD performs about the same as the RCD asymptotically, since in the long run RCD will each coordinate equally. However, if we narrow the search to the first few hundreds iterations, one can see that CCD is slightly lower on the loss value as shown below. As proved by Mert and etc., the Cyclic Coordinate Descent method should outperform RCD about 2 times faster if the Hessian is 2-cyclic matrix or M matrix.[^CCD]

![compare](/img/cse250/proj2_compare2.png)

## Critical Evaluation

There are many ways to improve the coordinate descent algorithm. Instead of single coordinate descent, we can update a block of coordinates[^block2]. The block coordinate descent is also proved to converge.[^block] There is also Gauss-Southwell rule that select the coordinate which maximize the gradient of the loss function, or Gauss-Southwell-Lipschitz rule that maximize the gradient of loss function over squared root of Lipschitzconstant, where both of them are proved to be faster than RCD.[^gauss-southwell]


[^CCD]: When Cyclic Coordinate Descent Outperforms Randomized Coordinate Descent, Mert Gürbüzbalaban, Asuman Ozdaglar†, Pablo A. Parrilo†, N. Denizcan Vanli†, https://papers.nips.cc/paper/7275-when-cyclic-coordinate-descent-outperforms-randomized-coordinate-descent.pdf

[^cooralgo]: Coordinate Descent Algorithms, Stephen J. Wright, http://www.optimization-online.org/DB_FILE/2014/12/4679.pdf

[^luotseng]: On the Convergence of the Coordinate Descent Method for Convex Differentiable Minimization, Z. Q. Luo, P. TSeng, https://link.springer.com/content/pdf/10.1007%2FBF00939948.pdf

[^block]: Convergence of a Block Coordinate Descent Method for Nondifferentiable Minimization, Tseng, P., https://doi.org/10.1023/A:1017501703105

[^block2]: Efficient Block-coordinate Descent Algorithms for the Group, Lasso, Zhiwei (Tony) Qin, Katya Scheinberg, Donald Goldfarb, http://www.optimization-online.org/DB_FILE/2010/11/2806.pdf

[^gauss-southwell]: Coordinate Descent Converges Faster with the Gauss-Southwell Rule Than Random Selectio, Julie Nutini, Mark Schmidt, Issam H. Laradji, Michael Friedlander, Hoyt Koepke, https://arxiv.org/abs/1506.00552

[^ubc]:  Coordinate Descent and Ascent Methods, Julie Nutini, https://www.cs.ubc.ca/~jnutini/documents/mlrg_CD.pdf

[^revival]: The Revival of Coordinate Descent Methods, Stephen Wright, https://engineering.jhu.edu/ams/wp-content/uploads/sites/44/2014/08/StephenWrightSlides112014.pdf#page=64&zoom=100,0,257
---
title: "Bayes Optimal Classifier"
date: 2019-01-31T18:00:14-08:00
categories: ["machine learning"]
series: ["statistical learning"]
tags: ["bayes", "notes"]
draft: false
---

## Background

[Marginal Distribution](../marginal-distribution)

Three ways to sample from P

1. Draw (x,y)
1. Draw y according to its marginal distribution, then x according to the conditional distribution of x | y
1. Draw X according to its marginal distribution, then Y according to the conditional distribution of y | x

Define:\
$\mu$: distribution on $X$\
$\eta$: conditional distribution y|x

## Classifier

**Normal Classifier**\
$h : x \rightarrow y$\
$R(h) = Pr_{(x,y) \in p} (h(x) \neq y)$, where R = risk

**Bayes Optimal Classifier**\
$h^* : x \rightarrow y$

\begin{equation}
  f(x)=\begin{cases}
    1 & \text{if $\eta(x) \geq \frac{1}{2}$} \newline
    0 & \text{otherwise}.
  \end{cases}
\end{equation}

$R(h^\*)$ should be minimum, so $R^\* = R(h^\*) = \mathbb{E}\_{x \in p}[min(\eta(x), 1 - \eta(x))]$

## Consistency

Algorithm is consitent if $R(h_n) \rightarrow R^*$ as $n \rightarrow \infty$

### Nearest Neighbor Classification

Pick n points at random from $P = (\mu, \eta)$\
Let $h_n$ be the 1-NN classifier based on these.
1-NN is not consistent.

e.g. consider the following distribution

- X = [0, 1], y = {0, 1}
- $\mu$ is uniform on X
- $\eta$ = 1/4 everywhere

Bayes optimal classifier

- $h^* = 0$
- $R^\*$ = 1/4

For 1-NN classifier

- Pr(error) = Pr(two coins of bias, 1/4 disagree) = 3/4 * 1/4 * 2 = 3/8 > $R^*$
- $R(h_n) = 2R^\* (1 - R^\*)$

For k-NN classifier, it's consistent ($R(h_{n,k}) \rightarrow R^*$) if

- k is grwoing fn of n with $k \rightarrow \infty$, $\frac{k}{n} \rightarrow \infty$
- $\eta$ is continuous

Proof

- if $\eta(x) = \frac{1}{2}$, then $R(h\_{n,k}) = 1 / 2$, $R(h^*) = 1 / 2$
- if $\eta(x) \lt 1 / 2$, and assume there is Ball B around x, Pr(inside B) = $\mu(B)$
![knn search radius](https://www.researchgate.net/profile/Kory_Allred/publication/280620610/figure/fig1/AS:284551587876865@1444853793479/Illustration-of-the-kNN-search-strategy-from-45-The-red-cross-indicates-the-point-to.png)
- As $n \rightarrow \infty$, graph become more dense, radius of B become smaller
  - Pr(k-NN of x fall in b) $\rightarrow$ 1 as $\frac{k}{n} \rightarrow 0$
  - Pr(majority voe of their label is 0) $\rightarrow$ 1 as $k_n \rightarrow \infty$
  - for example, $k(n) = \log n$

## Limitation

- All data i.i.d. from fixed unknown distribution over X x y
- Can't cover shifting distribution
  - $\mu$ changing, $\eta$ fixed(covariate shift): different handwriting/speech distribution
  - $\mu$, $\eta$ both change: classifying articles $\rightarrow$ politics, sports







---
title: "Prototype Selection"
date: 2019-01-27T20:25:22-08:00
categories: ["machine learning"]
series: ["statistical learning"]
tags: ["knn"]
draft: false
---

# Backgrond #
[kNN prototype selection](https://ieeexplore.ieee.org/document/6136515)
[Summary](https://sci2s.ugr.es/pr)
[List](https://sci2s.ugr.es/pr/pstax/techReport)

There are couple drawbacks for KNN

1. high storage for data
1. computation for decision boundary
1. intolerance to noise

There are couple methods address above issue

1. better similarity metric or better distance function
1. k-d trees or R-trees as storage
1. reduction technique (prototype selection)

Prototype Selection
1. edition method
  - remove noise
1. condensation method
  - remove superfluous dataset
1. hybrid method
  - achive elimination of noise and superfluous at the same time

# Methods #

## Edition Method ##

## Condensation Method ##
1. CNN
  - $S = {t_1, t2, ..., t_c}$
  - $T = Training Set \setminus S$
  - while there is misclassified point in T by training on S
     - for t in $T \setminus S$
         - if t is misclassified, S = S + {t}, T = T $\setminus$ {t}

1. [Protoype Selection by Clustering](https://ieeexplore.ieee.org/document/6377386)


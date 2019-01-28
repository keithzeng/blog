---
title: "Prototype Selection"
date: 2019-01-27T20:25:22-08:00
categories: ["machine learning"]
series: ["statistical learning"]
tags: ["knn"]
draft: false
---

[kNN prototype selection](https://ieeexplore.ieee.org/document/6136515)

There are couple drawbacks for KNN

1. high storage for data
1. computation for decision boundary
1. intolerance to noise

There are couple methods address above issue

1. better similarity metric
1. better distance function
1. k-d trees or R-trees as storage
1. reduction technique (prototype selection)

Prototype Selection
1. edition method
  - remove noise
1. condensation method
  - remove superfluous dataset
1. hybrid method
  - achive elimination of noise and superfluous at the same time
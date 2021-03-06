---
title: "Logistic Regression"
date: 2019-02-01T14:39:49-08:00
categories: ["machine learning"]
series: ["statistical learning"]
tags: ["logistic"]
draft: false
---

## Uncertainty in Prediction

Related to [Linear Regression](../logistic-regression).

The available features x do not contain enough information to perfectly predict y, such as

- x = medical record for patients at risk for a disease
- y = will he contact disease in next 5 years

## Model

We still going to use linear model for conditional probability estmation

$$w_1x_1 + w_2x_2 + ... + w_dx_d + b = w \cdot x + b$$

We want the Pr(y=1):

- increases as linear function grows
- 0.5 when linear function is 0

This leads to the sigmoid function

![sigmoid](/img/cse250/sigmoid.png)

## Logistic Regression Model
Let $y \in$ {-1, 1}

$$Pr(y = 1 | x) = \frac{1}{1 + e^{-(w \cdot x + b)}}$$

and

$$Pr(y = -1 | x) = 1 - Pr(y = 1 | x)  = \frac{1}{1 + e^{w \cdot x + b}}$$

Or consisely

$$Pr(y | x) = \frac{1}{1 + e^{-y(w \cdot x + b)}}$$

## Maximum-likelihood

We want to maximize the probability:

$$\prod_{i=1}^n Pr\_{w,b}(y^{(i)}|x^{(i)})$$

## Loss function

After taking log of maximum-likelihood formula, we convert it to the loss function

$$L(w, b) = - \sum\_{i=1}^n \ln Pr\_{w,b}(y^{(i)}|x^{(i)}) = \sum_{i=1}^n \ln (1 + e^{-y^{(i)}(w \cdot x^{(i)} + b)})$$

## Solution

There is no closed-form solution for w, but L(x) is convex.

Convexity is crucial because the local minimum is also the global minimum.

![convexity](/img/cse250/convexity.png)

We turn to numerical method gradient descent.

## Gradient Descent

1. Set $w_0 = 0$
1. For t = 0, 1, 2, ... until convergence:
  - $w_{t+1} = w_t + \eta_t \sum\_{i=1}^n y^{(i)}x^{(i)}Pr\_{w_t}(-y^{(i)} | x^{(i)})$, where $\eta_t$ is called step size (learning rate)




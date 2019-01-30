---
title: "Margin of Error"
date: 2019-01-27T22:33:16-08:00
categories: ["mathematic"]
series: ["statistical learning"]
tags: ["confidence interval", "statistic"]
draft: false
---

## Z-Score vs T-Score

### Z-Score
[Link](https://www.statisticshowto.datasciencecentral.com/probability-and-statistics/hypothesis-testing/t-score-vs-z-score/)

![When to Use T-Score vs Z-Score](https://www.statisticshowto.datasciencecentral.com/wp-content/uploads/2013/08/t-score-vs.-z-score.png)

Z-Score's formula
$$z = \frac{X - \mu}{\sigma}$$
where X = sample mean, $\mu$ = population means, $\sigma$ = population standard deviation.\
Also, we use Z Score when sample size >= 30 or we know the population's mean dna SD.

[Z Table](http://www.ltcconline.net/greenl/courses/201/estimation/smallConfLevelTable.htm)

### T-Score
[T-Score](https://www.statisticshowto.datasciencecentral.com/probability-and-statistics/t-distribution/t-score-formula/)
T-Score's formula
$$T = \frac{X - \mu}{s/ \sqrt{n}}$$
where X = sample mean, $\mu$ = population mean, s = sample standard deviation, and n = sample size.

[Formula for Margin of Eroor](https://www.statisticshowto.datasciencecentral.com/probability-and-statistics/hypothesis-testing/margin-of-error/)

### Margin of Error
They are two ways to find the margin of error
$$ME = Z \frac{\sigma}{\sqrt{n}}$$
Or if we know the population proportion
$$ME = Z \sqrt{\frac{p(1 - p)}{n}}$$
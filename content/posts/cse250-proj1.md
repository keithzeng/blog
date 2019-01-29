---
title: "CSE250 Proj1"
date: 2019-01-27T16:22:07-08:00
categories: ["machine learning"]
series: ["statistical learning"]
tags: ["CSE250B", "project", "mnist"]
draft: true
---

[HW 1](http://cseweb.ucsd.edu/classes/wi19/cse250B-a/prog1.pdf)

## 1. Prototype Selection ##
Divide data into ${S_1, S_2, ..., S_c}$, where c = number of labels. For each dataset $S_i$, I select M / c points as new training set for that label, which are the centroids by running k-means clustering algorithm.

My idea was to capture as many distinct types in for each label and meanwhile possibility reduce the noise near the boundary by selecting only the center of the type.

## 2. Pseudocode ##

### Top Level ###

create knnWrapper(dataX, dataY, neighbor, protype_num)

  - dataX = training data for X
  - dataY = label data for corresponding X
  - neighbor = number of closest neighbors picked to decide the query point
  - prototype_num = desired final data size

model = run wrapper knn(dataX, dataY, 1, M)

model.predict(query)

### Bottom Level ###

**Detailed implementation for function 'knnWrapper':**

$trainX = \emptyset$
$trainy = \emptyset$
labels = extra distinct labels from dataY
$data$ = group dataX by its label

for label in labels

  - centroids = find_k_means_clusters(data[label], M / C)
  - trainX = trainX + centroids
  - trainy append label M/C times

return knn(trainX, trainy, neighbor)

## 3. Experimental Results ##
The margin of error can be calculated using follwong
$$ME = Z\sqrt{\frac{p(1 -p)}{n}}$$
where Z is Z-value from [table](http://www.ltcconline.net/greenl/courses/201/estimation/smallConfLevelTable.htm) (=1.96 for 95% confidence interval), p = propotion mean of sample, n = sample size.

[Table Generator](https://www.tablesgenerator.com/markdown_tables)

| Num of Prototype |  Accuracy of Random | Accuracy of PS |
|-----------------:|--------------------:|---------------:|
|             1000 | 0.8841 $\pm$ 0.2008 |         0.9578 |
|             5000 | 0.9354 $\pm$ 0.1184 |         0.9697 |
|            10000 | 0.9484 $\pm$ 0.0959 |         0.9675 |

## 4. Critical Evaluation ##
My method is a improvement to the random selection. There are many more techniques for PS, such condensation, edition, and hybrid. I would love to try some of the hybrid methods that can further improve the performance.

Image credit to [sci2s](https://sci2s.ugr.es/pr) ![PS Methods](https://sci2s.ugr.es/sites/default/files/files/TematicWebSites/pr/psTaxonomy.png)

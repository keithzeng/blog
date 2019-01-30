---
title: "CSE250 Proj1"
date: 2019-01-27T16:22:07-08:00
categories: ["machine learning"]
series: ["statistical learning"]
tags: ["CSE250B", "project", "mnist"]
draft: true
---

[Project 1](http://cseweb.ucsd.edu/classes/wi19/cse250B-a/prog1.pdf)

## 1. Prototype Selection
Divide data into ${S_1, S_2, ..., S_c}$, where c = number of labels. For each dataset $S_i$, I select M/c points as new training set for that label, which are the centroids by running k-means clustering algorithm.

My idea was to capture as many distinct types in for each label and meanwhile reduce the noise by selecting only the center of the each type.

## 2. Pseudocode

create knnWrapper(dataX, dataY, neighbor, protype_num)

  - dataX = training data for X
  - dataY = label data for corresponding X
  - neighbor = number of closest neighbors picked to decide the query point
  - prototype_num = desired final data size

model = run knnWrapper(dataX, dataY, 1, M)

model.predict(query)

**Detailed Implementation for knnWrapper():**

$trainX = \emptyset$\
$trainy = \emptyset$\
labels = extra distinct labels from dataY\
$data$ = group dataX by its label\

for label in labels

  - centroids = find_k_means_clusters(data[label], M / C)
  - trainX = trainX + centroids
  - trainy append label M/C times

return knn(trainX, trainy, neighbor)

## 3. Experimental Results
The margin of error can be calculated according to [^lisa]
$$ME = Z\sqrt{\frac{p(1 -p)}{n}}$$
where

- Z is Z-value from z-table [^ztable], 1.96 chosen for 95% confidence interval
- p = proportion mean of sample
- n = sample size.

The plot for random selection for different M.
![Accuracy vs Prototye](/img/cse250/random_accuracy.png)

[Accuracy Random vs PS](https://www.tablesgenerator.com/markdown_tables)

| Num of Prototype |  Accuracy of Random | Accuracy of PS |
|-----------------:|--------------------:|---------------:|
|             1000 | 0.8841 $\pm$ 0.2008 |         0.9578 |
|             5000 | 0.9354 $\pm$ 0.1184 |         0.9697 |
|            10000 | 0.9484 $\pm$ 0.0959 |         0.9675 |



## 4. Critical Evaluation
My method is a improvement to the random selection. There are many more techniques for PS, such condensation, edition, and hybrid. I would love to try some of the hybrid methods that can further improve the performance,  for example Repeated Editing Fast Condensing Nearest Neighbour (RFCNN). Moreover, besides PS methods, they are approaches focusing on different aspect of problem for kNN. One aspect is looking at different dist function, such as Fast Similarity Search, Approximated Similarity Search, etc.[^jose] Also, one can also try differnt data structure for storing the points, such as vp-tree which provides O(logn) search time.[^peter]

Image credit to [sci2s](https://sci2s.ugr.es/pr) ![PS Methods](https://sci2s.ugr.es/sites/default/files/files/TematicWebSites/pr/psTaxonomy.png)

[^lisa]: Confidence Intervals for a Single Mean or Proportion, Lisa Sullivan, Wayne LaMorte, http://sphweb.bumc.bu.edu/otlt/MPH-Modules/QuantCore/PH717_ConfidenceIntervals-OneSample/PH717_ConfidenceIntervals-OneSample_print.html
[^ztable]: http://www.ltcconline.net/greenl/courses/201/estimation/smallConfLevelTable.htm
[^jose]: On the suitability of Prototype Selection methods for kNN classification with distributed data, Jose J. Valero-Mas, Jorge Calvo-Zaragoza, Juan R. Rico-Juan, https://grfia.dlsi.ua.es/repositori/grfia/pubs/341/SuitabilityPSDistributedScenarios.pdf
[^peter]: Data Structures and Algorithm for Nearest Neighbor Search in General Metric Spaces, Peter N. Yianilos, http://web.cs.iastate.edu/~honavar/nndatastructures.pdf


<!-- README.md is generated from README.Rmd. Please edit that file -->

# Kmeans

<!-- badges: start -->

![R-CMD-check](https://github.com/UBC-MDS/KmeansR/workflows/R-CMD-check/badge.svg)
[![codecov](https://codecov.io/gh/UBC-MDS/KmeansR/branch/master/graph/badge.svg)](https://codecov.io/gh/UBC-MDS/KmeansR)
<!-- badges: end -->

### Package description

This package consists of R functions that implement k-means clustering
from scratch. This will work on any dataset with valid numerical
features, and includes fit, predict, and clustersummary functions, as
well as elbow and silhouette methods for hyperparameter “k”
optimization. A high level overview of each function is given below. See
each function’s documentation for more details.

  - fit: This function classifies the non-labeled data into a given
    number of clusters k using the simple KMeans algorithm. It returns
    labels for each data point according to the cluster it belongs to
    and also cluster centers. This is a type of unsupervised learning
    method to classify data.

  - predict: Assigns each point in a dataset to a cluster. Dataset has
    to be in the same format as the original dataset the model was fit
    on.

  - elbow: Creates a plot of inertia vs number of cluster centers as per
    the elbow method. Calculates and returns the inertia values for all
    cluster centers. Useful for identifying the optimal number of
    clusters while using the k-means clustering algorithm.

  - silhouette: Returns the average silhouette score of each sample in a
    given 2-d array and clustering labels.

  - clustersummary: Provides summary of groups created from Kmeans
    clustering, including centroid coordinates, number of data points in
    training data assigned to each cluster, and within-cluster distance
    metrics.

There is a built-it k-means function in R. This package is not meant to
add to the existing ecosystem; but is rather intended to deepen
fundamental understanding of these algorithms.

## Installation

To use this pacakge, install the development version from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("UBC-MDS/Kmeans")
```

## Dependencies

  - tidyverse

## Usage

This is a basic example which shows you how to solve a common problem:

First, load the required pacakges and `fit` the data:

``` r
library(Kmeans)
library(tidyverse)
library(dplyr)

X = data.frame(x1 = c(1, 2, 3, 5, 53, 21, 43),
               x2 = c(1, 2, 3, 5, 53, 21, 43))
kmeans_results = fit(X, 2)
```

Use the fitted model to `predict` labels for new data:

``` r
X_new = data.frame(x1 = c(1, 4),
                   x2 = c(3, 2))
predict(X_new, kmeans_results$centers)
```

Use the `clustersummary` function to get information on the fitted
model:

    clustersummary(X, kmeans_results$centers, kmeans_results$labels)

If uncertain on the best value of k to choose, use the `elbow` and
`silhouette` functions:

    centers <- c(2, 3, 4, 5)
    inertia <- elbow(X, centers)$inertia
    
    k_vector <- c(2, 3, 4, 5)
    scores <- silhouette(X, k_vector)$scores

## Tests

To test that the functions work as intended, run `devtools::test()` in
the root of the project repo in an Rconsole.
